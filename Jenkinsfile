pipeline {
    agent any
    
    environment {
        // Replace with your actual Docker Hub username
        DOCKERHUB_USER = 'manju301'
        APP_NAME = 'my-web-app'
    }

    stages {
        stage('Clone Code') {
            steps {
                git credentialsId: 'git-hub', url: 'https://github.com/Manjulla14220/jenkins-docker'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKERHUB_USER/$APP_NAME:$BUILD_NUMBER .'
            }
        }

        stage('Login & Push to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'Manju$280', usernameVariable: 'manju301')]) {
                    sh "echo '$PASS' | docker login -u '$USER' --password-stdin"
                    sh "docker push ${DOCKERHUB_USER}/${APP_NAME}:${BUILD_NUMBER}"
                }
            }
        }

        stage('Cleanup') {
            steps {
                sh "docker rmi ${DOCKERHUB_USER}/${APP_NAME}:${BUILD_NUMBER}"
            }
        }
    }
}
