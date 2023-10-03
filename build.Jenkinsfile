pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')
                ]) {
                    sh '''
                    docker login --username $USERNAME --password $PASSWORD
                    docker build -t roberta:latest .
                    docker tag roberta:latest alonithuji/roberta:latest
                    docker push alonithuji/roberta:latest
                    '''
                }
            }
        }
        stage('Trigger Deploy') {
            steps {
                build job: 'RobertaDeploy', wait: false, parameters: [
                    string(name: 'ROBERTA_IMAGE_URL', value: "alonithuji/roberta:latest")
                ]
            }
        }
    }
}