pipeline{
    agent any
    stages{
        stage("code quality"){
            agent{docker'maven:3-alpine'}
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=muni \
  -Dsonar.host.url=http://18.217.76.135:9000 \
  -Dsonar.login=0258ee7c9295d0513be583f6a0922988ebf56e2c
                '''
            }
        }
        stage("code build"){
            agent{docker'maven:3-alpine'}
            steps{
                sh "mvn clean package"
            }
        }    
    }
}
