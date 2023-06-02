pipeline {
    
    agent any

    stages {
        
        stage('Build') {
            steps {
                echo 'Building'
                sh 'ls'
                sh 'docker info'
                sh 'docker image build -t jenkins-docker:2.401.1-lts .'
            }
        }
        
        stage('Pushing') {
            steps {
                sh 'docker images'
            }
        }
    }
}