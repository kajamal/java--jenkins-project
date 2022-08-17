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
  -Dsonar.host.url=http://3.95.181.64:9000 \
  -Dsonar.login=sqp_1b652e58a2325794aa56ce06da171a04d8acf2e6'
        }
        }
        stage("build Docker image"){
            steps{
               sh "docker build -t abbaskhan/works-with-heroku-2.0 ."



           }
         }
             stage("Docker deployement"){
              steps{
                 sh "docker run -d -p 8015:8080 abbaskhan/works-with-heroku-2.0"


            }
             }



       
    }
}

