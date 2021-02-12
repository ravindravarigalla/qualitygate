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
                     -Dsonar.projectKey=my-app \
                     -Dsonar.host.url=http://34.123.57.82:9000 \
                     -Dsonar.login=c2944e9d29259a3084d914591fa3a05d8d044d32
                     """
              }
            }
          }
         stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
      }
}   

  
    
  
                
  
  
