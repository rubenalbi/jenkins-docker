pipeline {
    
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub')
    }
    stages {
        
        stage('Build') {
            steps {
                echo 'Building'
                sh 'ls'
                sh 'docker info'
                sh 'docker image build -t rubenalbiach/jenkins-docker:2.401.1-lts .'
            }
        }
        
        stage('Push') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                sh 'docker push rubenalbiach/jenkins-docker:2.401.1-lts'  
            }
        }
    }
}