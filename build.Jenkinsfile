pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin 352708296901.dkr.ecr.eu-north-1.amazonaws.com
                docker build -t cicd-robera:latest .
                docker tag cicd-robera:latest 352708296901.dkr.ecr.eu-north-1.amazonaws.com/cicd-robera:latest
                docker push 352708296901.dkr.ecr.eu-north-1.amazonaws.com/cicd-robera:latest
                '''
            }
        }
    }
}