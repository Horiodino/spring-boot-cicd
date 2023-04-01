pipeline{
    agent any
    stages{
        stage('sonar quality status'){
            agent{
                docker{
                    image 'maven'
                }
            }

            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn clean package sonar:sonar '
                    }
                }
            }
        }

        stage('quality-gate status'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token'
                    }
                }
            }
        }
        stage('docker-build'){
            steps{
                script{
                    sh 'docker build -t maven-app .'
                }
            }
        }
    }
}