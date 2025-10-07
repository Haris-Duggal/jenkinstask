pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git branch: 'main', url: 'https://github.com/Haris-Duggal/jenkinstask.git'
            }
        }

        stage('Build') {
            steps {
                echo 'No build needed for static HTML site.'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying static files...'
                // Create output folder
                bat 'mkdir -p C:\\JenkinsOutput\\jenkinstask'

                // Copy all files
                bat 'xcopy * C:\\JenkinsOutput\\jenkinstask /E /H /Y'

                echo 'Website copied to C:\\JenkinsOutput\\jenkinstask'
            }
        }
    }
}
