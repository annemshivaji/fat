pipeline {
    agent any

    stages {
        stage('Checkout from Git') {
            steps {
                // Git checkout stage
                git credentialsId: 'your-git-credentials', url: 'https://github.com/yourusername/your-repo.git'
            }
        }

        stage('Build with Maven') {
            steps {
                // Maven build stage
                sh 'mvn clean install'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Docker build stage
                sh 'docker build -t your-image-name .'
            }
        }

        stage('Push to Docker Registry') {
            steps {
                // Docker push stage
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
                    sh 'docker push your-image-name'
                }
            }
        }
    }

    post {
        failure {
            // Error handling
            echo 'Pipeline failed! See logs for more details.'
            // You can add more detailed error handling/reporting here
        }
    }
}
