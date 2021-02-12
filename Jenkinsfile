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
                     -Dsonar.login=1eaac01ed337f35621a661df39369f8b8882d4e3
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

  
    
  
                
  
  
