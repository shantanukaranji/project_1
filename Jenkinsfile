



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
                sh 'mvn clean test'
                sh 'mvn package' 
            post {
                always {
                    junit '**/target/surefire-reports/*.xml' // Archive test results
                }
                failure {
                    echo " Tests failed! Check reports for details."
                }    
            }
}
}  
}        
