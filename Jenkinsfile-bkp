pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // This pulls your repo
                git branch: 'main', url: 'https://github.com/sangsana/ManCity.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mancity-trophies .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -itd --name mycont -p 1234:80 mancity-trophies'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                        sh 'docker tag mancity-trophies $DOCKER_USER/mancity-trophies:latest'
                        sh 'docker push $DOCKER_USER/mancity-trophies:latest'
                    }
                }    
            }
        }
    }
}
