pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image2 .'
            }
        }

        stage('Tag') {
            steps {
                sh 'docker tag image2 shaikmustafa/paytm:bus'
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub1') {
                        docker.image('shaikmustafa/paytm').push('bus')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f bus-app || true
                  docker run -itd --name bus-app -p 2222:80 shaikmustafa/paytm:bus
                '''
            }
        }
    }
}
