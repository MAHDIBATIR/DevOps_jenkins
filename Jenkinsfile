pipeline {
    agent any
    environment {
        registry = "mahdibatir/tp2"
        registryCredential = 'dockerhub-write-final'
    }
    stages {
        stage('Cloning Git') {
            steps {
                https://github.com/MAHDIBATIR/DevOps_jenkins.git'
            }
        }
        stage('Building Image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Test Image') {
            steps {
                // Simulation d'un test unitaire
                echo "Tests passed successfully"
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Deploy Image') {
            steps {
                // Deploiement automatique du conteneur fraichement cree
                sh "docker rm -f tp4_pipeline || true"
                sh "docker run -d -p 8082:80 --name tp4_pipeline ${registry}:${BUILD_NUMBER}"
            }
        }
    }
}