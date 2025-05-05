pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'yourdockerhubusername/html-cicd'
        DOCKER_CREDENTIALS_ID = 'docker-hub-creds' // Jenkins credentials ID
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/yourusername/html-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: env.DOCKER_CREDENTIALS_ID, usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh '''
                            echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin
                            docker push $DOCKER_IMAGE
                        '''
                    }
                }
            }
        }

        stage('Deploy (Optional)') {
            steps {
                echo 'Deployment step can be added here (e.g., SSH into server, pull and run container)'
            }
        }
    }
}
