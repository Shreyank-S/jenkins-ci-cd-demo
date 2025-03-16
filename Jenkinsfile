pipeline {
    agent any

    environment {
        REGISTRY = "localhost:5002"
        IMAGE_NAME = "myapp"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Shreyank-S/jenkins-ci-cd-demo'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $REGISTRY/$IMAGE_NAME:latest ./app'
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    sh 'docker run --rm $REGISTRY/$IMAGE_NAME:latest node -v'
                }
            }
        }

        stage('Push to Local Registry') {
            steps {
                script {
                    sh 'docker push $REGISTRY/$IMAGE_NAME:latest'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    sh 'docker run -d -p 8081:3000 $REGISTRY/$IMAGE_NAME:latest'
                }
            }
        }
        
        stage('Hello') {
            steps {
                echo 'Jenkinsfile is working!'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
