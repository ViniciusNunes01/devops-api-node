pipeline {
    agent any

    triggers {
        cron('0 3 * * *')
    }

    environment {
        IMAGE_NAME = 'projeto-api-node'
        CONTAINER_NAME = 'container-api-node'
        PORTA_HOST = '3000'
        PORTA_CONTAINER = '3000'
    }

    stages {
        stage('Limpeza (Cleanup)') {
            steps {
                script {
                    echo "Removendo container e imagem Node.js antigos se existirem..."
                    sh "docker rm -f ${CONTAINER_NAME} || true"
                    sh "docker rmi -f ${IMAGE_NAME} || true"
                }
            }
        }

        stage('Build da Imagem') {
            steps {
                echo "Construindo a nova imagem usando o Dockerfile do Node.js..."
                sh "docker build -t ${IMAGE_NAME} ."
            }
        }

        stage('Deploy do Container') {
            steps {
                echo "Inicializando o container Node.js..."
                sh "docker run -d --name ${CONTAINER_NAME} -p ${PORTA_HOST}:${PORTA_CONTAINER} ${IMAGE_NAME}"
            }
        }
    }
}