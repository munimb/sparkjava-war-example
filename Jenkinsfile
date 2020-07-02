pipeline{
    agent any
    stages{
        stage("code quality"){
            agent{docker'maven:3-alpine'}
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=red \
  -Dsonar.host.url=http://18.217.109.31:9000 \
  -Dsonar.login=df456b97fbe19933adafa1cbab1a0e496cd83f96
                '''
            }
        }
        stage("code build"){
            agent{docker'maven:3-alpine'}
            steps{
                sh "mvn clean package"
                rtUpload (
    serverId: 'artifactory',
    spec: '''{
          "files": [
            {
              "pattern": "**/sparkjava-hello-world-1.0.war",
              "target": "power/"
            }
         ]
    }''',
    buildName: 'power',
    buildNumber: '1'
)
            }
        }
        stage("deployment"){
            agent {label 'slave01'}
            steps {
            sh'''
            id
            pwd
            cd /home/jenkins/
            ls -lrt
            curl -uadmin:AP9EiJ33GJLc9SHUKyBszJBk371 -T "http://52.15.72.169:8081/artifactory/power/sparkjava-hello-world-1.0.war"
            cp sparkjava-hello-world-1.0.war /opt/tomcat/webapps/
                '''
            }
        }
    }
}
