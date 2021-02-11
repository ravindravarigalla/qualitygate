def getDockerTag(){
        def tag = sh script: 'git rev-parse HEAD', returnStdout: true
        return tag
        }

pipeline{
        agent any 
	environment{
	    Docker_tag = getDockerTag()
        }
        
	tools { 
        maven 'maven'  
    }
        
        stages{
          stage('Quality Gate Statuc Check'){
               steps{
                      script{
                      withSonarQubeEnv('sonar') { 
                      sh "mvn sonar:sonar"
                       }
                      timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
		       echo ${qg}	      
                      }
                    }
		    sh "mvn clean install"
                  }
                }  
              }
            }		
        }     	     
  
                
  
  
