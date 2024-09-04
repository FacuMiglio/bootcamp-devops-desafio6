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
                status=$sh 'ssh facu@192.168.100.20 sudo systemctl is-active apache2'
                if [ "$status" = "active" ]; then
                    echo "Apache2 está corriendo."
                else
                    echo "Apache2 no está corriendo."
                    echo "Instalando Apache2"
                    sh 'ssh facu@192.168.100.20 sudo apt update -y'
                    sh 'ssh facu@192.168.100.20 sudo apt install apache2 -y'
                    sh 'ssh facu@192.168.100.20 sudo apt systemctl start apache2'
                    sh 'ssh facu@192.168.100.20 sudo apt systemctl enable apache2'
                fi
                        
                }
                
                
                
                
                
                
            }
        }
        stage('Deploy to Apache') {
            steps {
                sh 'echo "<h1>Hello from Jenkins Pipeline 31/08/2024 22:46</h1> " '
            }
        }
    }

