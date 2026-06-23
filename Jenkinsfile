pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image3 .'
            }
        }

        stage('Tag') {
            steps {
                sh 'docker tag image3 shaikmustafa/paytm:movie'
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub1') {
                        docker.image('shaikmustafa/paytm').push('movie')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                  docker rm -f movie-app || true
                  docker run -itd --name movie-app -p 3333:80 shaikmustafa/paytm:movie
                '''
            }
        }
    }
}
