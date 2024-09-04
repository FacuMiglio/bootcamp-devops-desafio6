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
                sh '''#!/bin/bash
                    status=ssh facu@192.168.100.20 sudo systemctl is-active apache2
 
 
                if ( "$status" == "active" ){
                    echo "Apache2 está corriendo."
                    }
                else {
                    echo "Apache2 no está corriendo."
                    echo "Instalando Apache2"
                    ssh facu@192.168.100.20 sudo apt update -y
                    ssh facu@192.168.100.20 sudo apt install apache2 -y
                    ssh facu@192.168.100.20 sudo apt systemctl start apache2
                    ssh facu@192.168.100.20 sudo apt systemctl enable apache2
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

