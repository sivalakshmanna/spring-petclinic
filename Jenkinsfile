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
                sh 'mvn clean install -Dmaven.test.skip=true'
            }
        } 
        stage ('deploy the application') {
            steps {
                echo 'deploy the application'
                sh 'nohup java -jar target/*.jar > log.txt 2>&1 &'
            }
        } 
    }
    
    
}
