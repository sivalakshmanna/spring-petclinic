pipeline {
    agent any 
    stages {
        stage ('cloning the repository') {
            steps {
                echo 'cloning the repository'
                git branch:'main', url:'' 
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