pipeline{
    agent any
    stages{

        stage('sonar quality status'){
            agent{

                docker{
                    image 'maven:3.6.3-jdk-8'
                    args '-v /root/.m2:/root/.m2'
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