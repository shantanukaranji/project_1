




pipeline {
    agent any

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
    }
}
