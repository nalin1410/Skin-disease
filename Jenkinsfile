pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'nalin14102001/intrusion-detection-system:latest'
        DOCKER_CREDENTIALS_ID = 'docker-hub-credentials'
    }

    stages {
        stage('Initialize Git LFS') {
            steps {
                script {
                    // Ensure Git LFS is installed and initialized
                    sh 'git lfs install'
                }
            }
        }

        stage('Clone Repository') {
            steps {
                script {
                    // Clone the repository with Git LFS enabled
                    git branch: 'main', url: 'https://github.com/nalin1410/Skin-disease.git'
                    sh 'git lfs pull' // Fetch large files if any
                }
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
