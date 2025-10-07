pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                git branch: 'main', url: 'https://github.com/Haris-Duggal/jenkinstask.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    docker.build('jenkinstask-image')
                }
            }
        }

        stage('Run Container') {
            steps {
                echo 'Running Docker container...'
                script {
                    // Stop any running container with same name to avoid conflict
                    try {
                        sh 'docker stop jenkinstask-container || true'
                        sh 'docker rm jenkinstask-container || true'
                    } catch (err) {
                        echo "No existing container found. Continuing..."
                    }

                    // Run new container
                    sh 'docker run -d --name jenkinstask-container -p 3081:80 jenkinstask-image'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Deployment complete! Visit http://localhost:3081 to view your site.'
        }
        failure {
            echo '❌ Build failed. Check console output for details.'
        }
    }
}
