



pipeline {
    agent {
        node {
            label 'maven_node'
        }
    }

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-creds') // Store credentials securely in Jenkins
        IMAGE_NAME = "shantanukaranji/project_1"
        CONTAINER_NAME = "project_1_container"
        PORT_MAPPING = "8082:8082"
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
                    sh "docker login -u shantanukaranji -p \$DOCKERHUB_CREDENTIALS_PSW"
                    sh "docker push $IMAGE_NAME"
                }
            }
        }

        stage('Deploy Container') {
            steps {
                // Stop and remove existing container if it's running
                sh "docker stop $CONTAINER_NAME || true"
                sh "docker rm $CONTAINER_NAME || true"

                // Run the new container
                sh "docker run -d --name $CONTAINER_NAME -p $PORT_MAPPING $IMAGE_NAME"
            }
        }
    }
}

