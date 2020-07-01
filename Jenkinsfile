pipeline{
    agent any
    stages{
        stage("code quality"){
            agent{docker'maven:3-alpine'}
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=yellow \
  -Dsonar.host.url=http://18.191.174.227:9000 \
  -Dsonar.login=40a100e32ba1c80445b8b725a75332245dc11e63
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
