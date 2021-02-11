pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonar') {
                sh """
                   mvn sonar:sonar \
                     -Dsonar.projectKey=frontend \
                     -Dsonar.host.url=http://34.123.57.82:9000 \
                     -Dsonar.login=new
              }
            }
          }
         stage("Quality gate") {
            steps {
                waitForQualityGate abortPipeline: true
            }
          }
        }
      }
  
