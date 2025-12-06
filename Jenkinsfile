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
      telegramSend(message: "✅ Build #${BUILD_NUMBER} SUCCESS\nJob: ${JOB_NAME}\nDuration: ${currentBuild.durationString}", chatId: 396976151)
    }
    failure {
      telegramSend(message: "❌ Build #${BUILD_NUMBER} FAILED\nJob: ${JOB_NAME}", chatId: 396976151)
    }
  }
}
