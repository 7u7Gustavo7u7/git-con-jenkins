pipeline {
    agent any

    stages {
        stage('Obtener código') {
            steps {
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/gamiMTZ/ejemplopipeline.git'
            }
        }

        stage('Compilar código') {
            steps {
                echo 'Inicio de compilación del código'
                // Check if javac is available
                sh 'which javac  echo "javac not found"'
                // Compile Java program
                sh 'javac Programa.java  echo "javac failed"'
                echo 'Fin de compilación del código'

                echo 'Ejecución del código en python'
                // Check if python3 is available
                sh 'which python3  echo "python3 not found"'
                // Run Python script
                sh 'python3 Programa.py  echo "python3 execution failed"'
            }
        }

        stage('Test') {
            steps {
                script {
                    // Search for the method showInConsole in Programa.java
                    def result = sh(script: 'grep -q "mostrarEnConsola()" Programa.java', returnStatus: true)
                    if (result != 0) {
                        error('Method mostrarEnConsola() not found in Programa.java')
                    } else {
                        echo 'Method mostrarEnConsola() found in Programa.java'
                    }
                }
            }
        }

        stage("Ejecución") {
            steps {
                echo 'Ejecutando programa'
                // Run the compiled Java program
                sh 'java Programa || echo "java execution failed"'
            }
        }
    }
}
