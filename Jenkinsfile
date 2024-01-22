pipeline {
    tools {
        maven 'Maven'
    }
    agent any
    
    stages {
        stage('Build Maven') {
            steps {
                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Ensure Docker can run without sudo in your Jenkins environment
                    sh 'docker build -t shivangkataria/my-app-1.0 .'
                }
            }
        }
        stage('Push Docker Image') {
            steps{
                script {
                    withCredentials([string(credentialsId: 'shivangkataria', variable: 'shivangkataria')]) {
                        sh 'docker login -u shivangkataria -p ${shivangkataria}'
                        
                        sh 'docker push shivangkataria/my-app-1.0'
}
                }
            }
        }
    }
}
