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
                    docker tag roberta:latest avnichauhan/roberta:latest
                    docker push avnichauhan/roberta:latest
                    '''
                }
            }
            post {
               always {
                 sh '''
                 docker image prune -f -a --filter "until=240h"
                 '''
               }

            }
        }
        stage('Trigger Deploy') {
            steps {
                build job: 'RobertaDeploy', wait: false, parameters: [
                    string(name: 'ROBERTA_IMAGE_URL', value: "avnichauhan/roberta:latest")
                ]
            }

        }

    }
}