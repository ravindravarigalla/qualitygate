pipeline {

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
    stages {
        stage('Clone sources') {
            steps {
                git branch: 'bad-code', url: 'https://github.com/tkgregory/sonarqube-jacoco-code-coverage.git'
            }
        }
        stage('SonarQube analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "./gradlew sonarqube"
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
} 

  
  
