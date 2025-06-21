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
                        
                           mvn clean verify sonar:sonar \
                          -Dsonar.projectKey=jenkins \
                          -Dsonar.host.url=http://34.61.168.75:9000 \
                          -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }
        stage ('docker build') {
            steps {
                echo 'docker build springpetclinic'
                sh 'java -jar target/*.jar'
            
            }
        } 
    }
    
    
}
