pipeline {
    agent any

    environment {

    REGISTRY_URL = '352708296901.dkr.ecr.eu-north-1.amazonaws.com'

    }

    stages {
        stage('Build') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')
                ]) {
                    sh '''
                    docker login --username $USERNAME --password $PASSWORD
                    docker build -t cicd-robera:latest .
                    docker tag cicd-robera:latest $REGISTRY_URL/cicd-robera:latest
                    docker push $REGISTRY_URL/cicd-robera:latest
                    '''
                }
            }
        }
    }
}