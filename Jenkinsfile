pipeline {
    agent any
    tools {
       maven 'maven8'
    }
    stages {
        stage("git clone"){
            steps{
                git 'https://github.com/Abbas811/java--jenkins-project_sonar.git'
            }

        }
        stage("build code"){
            steps{
                sh "mvn clean install"
        }
        }
        stage("sonar"){
            steps{
           sh 'mvn clean verify sonar:sonar \
  -Dsonar.projectKey=ak_sonar \
  -Dsonar.host.url=http://52.23.230.225:9000 \
  -Dsonar.login=sqp_01c7994be42b2066f7b5337da988bd9b6de2a19b'
        }
        }
        stage("build Docker image"){
            steps{
               sh "docker build -t abbaskhan1/works-with-heroku-2.0 ."



           }
         }
             stage("Docker deployement"){
              steps{
                 sh "docker run -d -p 8018:8080 abbaskhan2/works-with-heroku-2.0"


            }
             }
        stage('nexus upload'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'works-with-heroku', classifier: '', file: 'target/works-with-heroku-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'ak_nexus', groupId: 'works.buddy.samples', nexusUrl: '34.224.215.33:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'



       
    }
}
        stage('tomcat deploy'){
            steps{
                sshagent(['nex_tom']) {
                    sh "scp -o StrictHostKeyChecking=no target/works-with-heroku-1.0-SNAPSHOT.war ubuntu@34.224.215.33:/home/ubuntu/apache-tomcat-8.5.82/webapps"

    
}
    }
}
    }
}
