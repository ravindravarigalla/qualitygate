pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage ("SonarQube analysis") {
            steps {
             withSonarQubeEnv('SonarQube') {
           sh "../../../sonar-scanner-2.9.0.670/bin/sonar-scanner"   
      }

      def qualitygate = waitForQualityGate()
      if (qualitygate.status != "OK") {
         error "Pipeline aborted due to quality gate coverage failure: ${qualitygate.status}"
      }
   }
}      
        }
    }
    
                
  
  
