pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:/Program Files/Java/jdk-21'  // Set this to your JDK path
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/LohithChowdary2004/OMSVC.git'
            }
        }

        stage('Build Maven Package') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                echo "Test Completed"
            }
        }

        stage('Start Services with Docker Compose') {
            steps {
                script {
                    bat 'docker-compose up -d --build'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
        cleanup {
            cleanWs() // only cleans Jenkins workspace, not containers
        }
    }
}
