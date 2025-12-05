pipeline {
  agent any

  tools {
    maven 'Maven 3.9' // Specify the Maven installation name configured in Jenkins
  }

  stages {
    stage('Build') {
      steps {
        dir('complete') {
          sh 'mvn clean install'
        }
      }
    }
  }

  post {
    success {
      archiveArtifacts artifacts: 'complete/target/*.jar'
    }
  }
}
