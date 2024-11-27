pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nalin14102001/intrusion-detection-system:latest'
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/nalin1410/Skin-disease.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push Docker Image to Hub') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', env.DOCKER_CREDENTIALS_ID) {
                        docker.image(env.DOCKER_IMAGE).push()
                    }
                }
            }
        }
    }
}