pipeline{
    agent any
    environment{
        GIT_REPO = 'https://github.com/Abhishek3807/test'
        BRANCH = 'main'
    }
    stages {
        stage('Clone'){
            steps{
                git branch : "${BRANCH}" , url : "${GIT_REPO}"
            }
        }
        stage('Build Docker Image'){
            steps{
                echo 'Building docker image for html page'
                bat 'docker build -t static-html-site .'
            }
        }
        stage('Deploy docker container'){
            steps{
                echo 'stopping old container if exists'
                bat 'docker rm -f html-container || exho "no container to remove"' 

                echo "running new container"
                bat 'docker run -d -p 8085:80 --name html-container static-html-site'
            }
        }
    }
    post{
        success{
            echo 'static html site deployed successfully!'
        }
        failure{
            echo 'pipeline failed!'
        }
    }

}
