pipeline {
  agent any

  tools {
      maven 'Maven 3.9' // Specify the Maven installation name configured in Jenkins
  }

  environment {
      TELEGRAM_TOKEN = credentials('telegram-token')
      TELEGRAM_CHAT_ID = credentials('telegram-chat-id')
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
          sh '''
              curl -s -X POST https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage -d chat_id=${TELEGRAM_CHAT_ID} -d text="✅ Build #${BUILD_NUMBER} SUCCESS - ${JOB_NAME}"
          '''
      }
      failure {
          sh '''
              curl -s -X POST https://api.telegram.org/bot${TELEGRAM_TOKEN}/sendMessage -d chat_id=${TELEGRAM_CHAT_ID} -d text="❌ Build #${BUILD_NUMBER} FAILED - ${JOB_NAME}"
          '''
      }
  }
}