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
                     -Dsonar.login=e567ff410914cba833593e9d78c6128f58010102
                     """
              }
            }
          }
         stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
      }
}   
  
