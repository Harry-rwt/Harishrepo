
peline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('rawatji')  // Use your Jenkins credentials ID
    }

    stages {
        stage('SCM Checkout') {
            steps {
                // Checkout code from GiitHub repository
                git 'https://github.com/Harry-rwt/docker_project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image with the dynamic tag using the Jenkins build number
                sh 'docker build -t Harry-in/harishimage:$BUILD_NUMBER .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                // Login to Docker Hub using credentials stored in Jenkins
                withCredentials([usernamePassword(credentialsId: 'icep-dockerhub', usernameVariable: 'DOCKERHUB_CREDENTIALS_USR', passwordVariable: 'DOCKERHUB_CREDENTIALS_PSW')]) {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                // Push the Docker image to Docker Hub
                sh 'docker push harry-in/harishimage:$BUILD_NUMBER'
            }
        }
    }

    post {
        always {
            // Clean up Docker resources after the build
            sh 'docker system prune -f'
        }
    }
}
sword-stdin'dd
