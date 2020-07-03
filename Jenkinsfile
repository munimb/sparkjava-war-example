pipeline{
    agent any
    stages{
        stage("code quality"){
            agent{docker'maven:3-alpine'}
            steps{
                sh '''
                mvn sonar:sonar \
  -Dsonar.projectKey=red \
  -Dsonar.host.url=http://3.133.108.239:9000 \
  -Dsonar.login=5c7c1d832e3fa7bad9ed8c4a9f41bc3b9134212a
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
              "target": "project/"
            }
         ]
    }''',
    buildName: 'project',
    buildNumber: '1'
)
            }
        }
    }
}
