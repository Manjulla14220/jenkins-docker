pipeline {
    agent any
    environment {
        // Replace with your actual Docker Hub username
        DOCKERHUB_USER = 'manju301'
        APP_NAME = 'my-web-application7'
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
                withCredentials([usernamePassword(credentialsId: 'docker-hub', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                    sh "echo '${DOCKER_PASS}' | docker login -u '${DOCKER_USER}' --password-stdin"
                    sh "docker push ${DOCKERHUB_USER}/${APP_NAME}:${BUILD_NUMBER}"
                }
            }

        }
      stage('Deploy to Host') {
          steps {
              sh '''
                  docker pull $DOCKERHUB_USER/$APP_NAME:$BUILD_NUMBER
                  docker create --name temp_container1234567 $DOCKERHUB_USER/$APP_NAME:$BUILD_NUMBER
                  docker cp temp_container1234567:/usr/share/nginx/html/index.html /usr/share/nginx/html/
                  docker rm temp_container1234567
                 '''
    }
}
        }


    }

