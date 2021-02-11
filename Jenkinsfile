pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage("build & SonarQube analysis") {
            steps{
                      script{
                      withSonarQubeEnv('sonar') { 
                      sh "mvn sonar:sonar"
                       }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }
		    sh "mvn clean install"
                  }
      }
}   
  
                
  
  
