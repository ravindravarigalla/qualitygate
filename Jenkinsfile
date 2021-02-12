pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('SonarQube') {
                sh """
                   mvn sonar:sonar 
                     """
              }
            }
          }
         stage("Quality Gate") {
            steps {
                waitForQualityGate abortPipeline: true
              }
            }
          }
      }
  
  
                
  
  
