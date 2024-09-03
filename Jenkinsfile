pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/TuUsuario/web-deploy.git'
            }
        }
        stage('Check Apache') {
            steps {
                sh 'echo "Verificando instalación de Apache...."'
                
            }
        }
        stage('Deploy to Apache') {
            steps {
                sh 'echo "<h1>Hello from Jenkins Pipeline 31/08/2024 22:46</h1> " '
            }
        }
        post {
            always {
                cleanWs()
            }
        }
    }
}
