pipeline {

  environment {
    IMAGE_TAG = "trainingad1/ms-ref-service-a"
    JENKINS_CRED = "${PROJECT}"
  }

  agent {
    kubernetes {
      
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  
  containers: 
  - name: maven
    image: maven:3.3.9
    imagePullPolicy: IfNotPresent
    command:
    - cat
    tty: true 
  
    
"""
}
  }
  stages {
    stage('build') {
      steps {
          withSonarQubeEnv('SonarQube') {
        container('maven') {
          sh """
            #echo "******** currently executing Build stage ********"
            mvn sonar:sonar 
          """
        }
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


