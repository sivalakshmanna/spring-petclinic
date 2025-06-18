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
                sh 'mvn package'
            }
        }  
    }
}
