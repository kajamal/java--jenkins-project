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
  -Dsonar.projectKey=ak1_sonar \
  -Dsonar.host.url=http://34.230.17.68:9000 \
  -Dsonar.login=sqp_26a70f8efca0e4998f5282f53882d8cc25880f92'
        }
        }
        stage("build Docker image"){
            steps{
               sh "docker build -t abbaskhan1/works-with-heroku-2.0 ."



           }
         }
             stage("Docker deployement"){
              steps{
                 sh "docker run -d -p 8016:8080 abbaskhan1/works-with-heroku-2.0"


            }
             }
        stage('nexus upload'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'works-with-heroku', classifier: '', file: 'target/works-with-heroku-1.0-SNAPSHOT.war', type: 'war']], credentialsId: 'ak_nexus', groupId: 'works.buddy.samples', nexusUrl: '34.224.215.33:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'



       
    }
}
    }
}
