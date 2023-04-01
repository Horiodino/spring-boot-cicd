pipeline{
    agent any
    stages{
        stage('docker-permission'){
            steps{
                script{
                    sh 'sudo docker chmod 777 /var/run/docker.sock'
                }
            }
        }

        stage('sonar quality status'){
            agent{
                docker{
                    image 'maven:3.6.3-jdk-8-slim'
                }
            }

            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }
    }
}