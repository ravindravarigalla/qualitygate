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
            mvn sonar:sonar \
              -Dsonar.projectKey=maven \
              -Dsonar.host.url=http://147.139.132.232:9000 \
              -Dsonar.login=576ac1441833e84cc6577e544fe4605ca7b48161
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


