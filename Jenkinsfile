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
                    bat 'docker stop jenkinstask-container || exit 0'
                    bat 'docker rm jenkinstask-container || exit 0'
                    bat 'docker run -d --name jenkinstask-container -p 3081:80 jenkinstask-image'
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
