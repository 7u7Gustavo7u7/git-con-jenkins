pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 50000:50000'
        }
    }

    environment {
        registry = "7u7gustavo7u7/repositorio_produccion"
        registryCredential = 'edec5687-20f9-4c33-9118-e70d1f5be7f9'
        dockerImage = ''
    }

    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'chmod +rx ./jenkins/scripts/*.sh'
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: '¿Continuar con la etapa de Deploy? (Haz clic en "Proceed" para continuar)'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:${env.BUILD_ID}")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: '¿Finalizar el uso de React App? (Haz clic en "Proceed" para finalizar)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
