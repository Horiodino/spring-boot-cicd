pipeline{
    agent any
    stages{

        stage('sonar quality status'){
            agent{

                docker{
                    sh 'chmod 777 /var/run/docker.sock'
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