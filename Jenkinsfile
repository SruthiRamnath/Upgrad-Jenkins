pipeline{
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '2'))
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }
    stages{
        stage('Git Checkout') {
        steps {
                checkout scm
            }
        }

        stage('Build'){
            steps{
                sh 'docker build -t node_app .'
                sh 'docker tag node_app:latest 434499784614.dkr.ecr.us-east-1.amazonaws.com/node_app:latest'
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 434499784614.dkr.ecr.us-east-1.amazonaws.com'
                sh 'docker push 434499784614.dkr.ecr.us-east-1.amazonaws.com/node_app:latest'
            }
        }
        
    }
}