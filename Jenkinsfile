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
                    withDockerRegistry(credentialsId: 'dockerhub-creds') {
                        sh 'docker tag mancity-trophies sangsana/Puli:latest'
                        sh 'docker push sangsana/Puli:latest'                                          // some block
                    }
                }
            }    
        }
    }
}
