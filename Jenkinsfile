pipeline {
    agent any
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
			     sh 'docker run -d -p 9090:8080 sivalakshmanna/springpetclinic:${BUILD_NUMBER}'	 
                         } 
                }
            }  
    }
    }   
}
