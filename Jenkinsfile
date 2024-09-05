pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Clonar el repositorio desde GitHub en la rama main
                git branch: 'main', url: 'https://github.com/FacuMiglio/bootcamp-devops-desafio6.git'
            }
        }

        stage('Check Apache') {
            steps {
                echo "Verificando instalación de Apache"
                sshagent(credentials: ['4c2ca7fd-35ca-47e2-a54d-5f6d05e4c3a1']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no facu@192.168.100.20 << EOF
                            status=$(systemctl is-active apache2)
                            if [ "$status" = "active" ]; then
                                echo "Apache2 está corriendo."
                            else
                                echo "Apache2 no está corriendo. Instalando Apache2..."
                                sudo apt update -y
                                sudo apt install apache2 -y
                                sudo systemctl start apache2
                                sudo systemctl enable apache2
                            fi
                        EOF
                    '''
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                echo "Desplegando aplicación en Apache"
                sshagent(credentials: ['4c2ca7fd-35ca-47e2-a54d-5f6d05e4c3a1']) {
                    sh '''
                        ssh -o StrictHostKeyChecking=no facu@192.168.100.20 << EOF
                            # Clonar el repositorio y copiar el index.html al directorio web
                            git clone https://github.com/FacuMiglio/bootcamp-devops-desafio6.git
                            sudo cp bootcamp-devops-desafio6/index.html /var/www/html/index.html
                            sudo rm -rf bootcamp-devops-desafio6
                            sudo systemctl restart apache2
                        EOF
                    '''
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline completado."
        }
        success {
            echo "Despliegue realizado con éxito."
        }
        failure {
            echo "Error en el despliegue."
        }
    }
}
