pipeline {
environment {
registry = "arramsyah/docker-rest-api-app"
registryCredential = 'edec5687-20f9-4c33-9118-e70d1f5be7f9'
dockerImage = ''
}
agent any

    stages {
        stage('Checkout') {
            steps {
                // Clona el repositorio desde GitHub
                git branch:"main", url: 'https://github.com/7u7Gustavo7u7/git-con-jenkins.git'
            }
        }

        stage('Compile') {
            steps {
                script {
                    // Verifica si el archivo HolaMundo.java existe
                    if (fileExists('holamundo.java')) {
                        echo 'Compiling HolaMundo.java'
                        // Compila el archivo Java
                        sh 'javac holamundo.java'
                    } else {
                        error 'File HolaMundo.java not found'
                    }
                }
            }
        }

   stage('Test') {
            steps {
                script {
                    // Search for the method showInConsole in Programa.java
                    def result = sh(script: 'grep -q "mostrarEnConsola()" holamundo.java', returnStatus: true)
                    if (result != 0) {
                        error('Method mostrarEnConsola() not found in holamundo.java')
                    } else {
                        echo 'Method mostrarEnConsola() found in holamundo.java'
                    }
                }
            }
        }
    }
}
