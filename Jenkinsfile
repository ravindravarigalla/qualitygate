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
              -Dsonar.projectKey=adservice \
              -Dsonar.host.url=http://34.123.57.82:9000 \
              -Dsonar.login=1836b6c41719b780d9ad485de6f364e3dc8e9aa4
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


