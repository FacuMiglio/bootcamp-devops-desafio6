pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/FacuMiglio/bootcamp-devops-desafio6.git'
            }
        }
        stage('Check Apache') {
            steps {
                sh 'echo "Verificando instalación de Apache"'
                sshagent(['4c2ca7fd-35ca-47e2-a54d-5f6d05e4c3a1']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no facu@192.168.100.20
                        status=$(systemctl is-active apache2)
                        if ( "$status" == "active" ); then {
                            echo "Apache2 está corriendo."
                        }
                        else {
                            echo "Apache2 no está corriendo."
                            echo "Instalando Apache2"
                            sudo apt update -y
                            sudo apt install apache2 -y
                            sudo systemctl start apache2
                            sudo systemctl enable apache2
                        fi
                    }'''
  
                }
            }
        }
        stage('Deploy to Apache') {
            steps {
                sh 'echo "<h1>Hello from Jenkins Pipeline 31/08/2024 22:46</h1> " '
            }
        }
    }
}
