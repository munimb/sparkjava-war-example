pipeline{
    agent any
    stages{
        stage("code quality"){
            agent{docker'maven:3-alpine'}
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=reddy \
  -Dsonar.host.url=http://18.217.76.135:9000 \
  -Dsonar.login=0b2bd03cb6237c453b98ea0f6673ccf458d8cd9b
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
