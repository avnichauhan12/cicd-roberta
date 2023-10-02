pipeline {
    agent any

    environment {

    REGISTRY_URL = '352708296901.dkr.ecr.eu-north-1.amazonaws.com'

    }

    stages {
        stage('Build') {
            steps {
                sh '''
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin $REGISTRY_URL
                docker build -t cicd-robera:latest .
                docker tag cicd-robera:latest $REGISTRY_URL/cicd-robera:latest
                docker push $REGISTRY_URL/cicd-robera:latest
                '''
            }
        }
    }
}