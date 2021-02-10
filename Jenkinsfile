pipeline {
        agent any
        tools { 
        maven 'maven'  
    }
        stages {
          stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonar') {
                sh 'mvn clean package sonar:sonar'
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
