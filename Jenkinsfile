pipeline {
    agent any

    environment {
        PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;C:\\Program Files\\IBM\\Cloud\\bin;C:\\Windows\\System32"
    
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Anitha-Pal/config-management.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    bat """
                    echo 🔨 Building Docker Image...
                    docker build -t config-manage:latest -f docker/Dockerfile .
                    """
                }
            }
        }
stage('Remove Existing Container') {
            steps {
                script {
                    bat """
                    echo 🧹 Checking if old container exists...
                    docker stop %CONTAINER_NAME% || echo Container not running
                    docker rm %CONTAINER_NAME% || echo Container not found
                    """
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    bat """
                    echo 🚀 Running Docker Container...
                    docker run -d -p 8083:83 --name %CONTAINER_NAME% %IMAGE_NAME%:latest
                    """
                }
            }
        }
    }
       
    post {
        success {
            echo '✅ Pipeline completed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}  // 🔹 Closes `pipeline`
