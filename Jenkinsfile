




pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds') // Store credentials securely in Jenkins
        IMAGE_NAME = "shantanukaranji/project_1"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git credentialsId: 'github-credentials', branch: 'main', url: 'https://github.com/shantanukaranji/project_1.git'

            }
        }

        stage('Test Code') {
            steps {
                sh 'mvn clean package' 
        }
        }    

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    sh "docker login -u shant -p \$DOCKERHUB_CREDENTIALS_PSW"
                    sh "docker push $IMAGE_NAME"
                }
            }
        }
    }
}
