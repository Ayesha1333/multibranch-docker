pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image1 .'
            }
        }

        stage('Tag') {
            steps {
                sh 'docker tag image1 shaikmustafa/paytm:bank'
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub1') {
                        docker.image('shaikmustafa/paytm:bank').push()
                    }
               }
          }
     }

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f bank-app || true
                  docker run -itd --name bank-app -p 1111:80 shaikmustafa/paytm:bank
                '''
            }
        }
    }
}
