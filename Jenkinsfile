pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage ("SonarQube analysis") {
             steps {
                withSonarQubeEnv('SonarQube') {
                  sh """
                     mvn sonar:sonar \
                       -Dsonar.projectKey=frontend \
                       -Dsonar.host.url=http://34.123.57.82:9000 \
                       -Dsonar.login=e567ff410914cba833593e9d78c6128f58010102
                     """
      }

      def qualitygate = waitForQualityGate()
      if (qualitygate.status != "OK") {
         error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
          }
        }
      }            
  }
}   
  
