pipeline {
    agent any
    environment {
        registry = "Dantrag2609/test"
        registryCredential = 'H0ly$m0ke36918'
        dockerImage = ''
    }
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Dantrag2609/MyFirstRepo.git'
            }
        }
        stage('Build Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleanup') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}
