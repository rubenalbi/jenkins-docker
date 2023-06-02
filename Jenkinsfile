pipeline {
    
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub')
        TAG_VERSION = '2.401.1-lts'
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building'
                sh 'ls'
                sh 'docker info'
                sh 'docker image build -t rubenalbiach/jenkins-docker:$TAG_VERSION --build-arg TAG=$TAG_VERSION .'
            }
        }
        stage('Push') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push rubenalbiach/jenkins-docker:$TAG_VERSION'  
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
        failure {
            mail to: 'ruben.albiach@gmail.com',
            subject: "[Jenkins] ${currentBuild.currentResult} ${env.JOB_NAME}",
            body: " ${currentBuild.currentResult}.\n Ha fallado la generación de la imagen de jenkins docker: ${env.BUILD_URL}"
        }
  }
}