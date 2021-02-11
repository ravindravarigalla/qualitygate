pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage('SonarQube analysis') {
            steps {      
              withSonarQubeEnv('Sonar') {
                 sh 'mvn clean package sonar:sonar'
    } // SonarQube taskId is automatically attached to the pipeline context
  }
}
                
         stage("Quality Gate"){     
             timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
             def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
             if (qg.status != 'OK') {
                 error "Pipeline aborted due to quality gate failure: ${qg.status}"
           }
         }
      }
     }
    }
    
                
  
  
