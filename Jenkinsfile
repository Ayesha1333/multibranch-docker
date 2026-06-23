pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build -t image3 .'
            }
        }
        stage ("Tag") {
            steps {
                sh 'docker tag image3 shaikmustafa/paytm:movie'
            }
        }
        stage('Push') {
            steps {
                scrpit {
                    withDockerRegistry(credentialsId: 'dockerhub1') {
                        sh 'docker push shaikmustafa/paytm:movie'
                    }
                }
            }
        }
        
        stage ("Deploy") {
            steps {
                sh 'docker run -itd --name movie-app -p 3333:80 shaikmustafa/paytm:movie'
            }
        }
    }
}
