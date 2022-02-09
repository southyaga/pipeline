pipeline {
  agent { label 'linux' }
  options {
    buildDiscarder(logRotator(numToKeepStr: '5'))
  }
  environment {
    DOCKERHUB_CREDENTIALS = credentials('ea7d5977-7945-47c0-be5c-3933e4b54977-dockerhub')
  }
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t southyaga/stws-alpine:latest .'
      }
    }
    stage('Login') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
      }
    }
    stage('Push') {
      steps {
        sh 'docker push southyaga/stws-alpine:latest'
      }
    }
  }
  post {
    always {
      sh 'docker logout'
    }
  }
}

