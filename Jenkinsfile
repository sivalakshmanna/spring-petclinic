pipeline {
    agent any
    environment {
        SONAR_TOKEN = credentials('sonar')  // Fetch the token from Jenkins credentials
    }    
    tools {
    maven 'maven'
  }
    stages {
        stage ('cloning the repository') {
            steps {
                echo 'cloning the repository'
                git branch:'main', url:'https://github.com/sivalakshmanna/spring-petclinic.git' 
                sh 'ls'
            }
        }
       
        stage ('building the application') {
            steps {
                echo 'build the application'
                sh 'mvn clean package'
            }
        } 
       stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {  // Name of SonarQube server configured in Jenkins
                    sh """
                         mvn sonar:sonar \
                        -Dsonar.projectKey=jenkins \
                        -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    echo 'docker image build'
		            echo "local-storage"
	                sh 'docker build -t sivalakshmanna/springpetclinic:${BUILD_NUMBER} .'
                }
            }
        }		
        		
	    stage('Push image to Hub'){
            steps{
                   
		   script {
                         withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                             sh "docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD"
                             sh 'docker push sivalakshmanna/springpetclinic:${BUILD_NUMBER}'
			     sh 'docker run --name spring-petclinic -d -p 9090:8080 sivalakshmanna/springpetclinic:${BUILD_NUMBER}'	 
                         } 
                }
            }  
    }
    }   
}
