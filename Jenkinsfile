pipeline {
  agent any
  stages {
    stage('Clean UP') {
      steps {
        cleanWs()
      }
    }
    stage('Code Clone') {
      steps {
        git branch: 'main', url: 'https://github.com/iemafzalhassan/full-stack_chatApp.git'
      }
    }
    stage('Build') {
      steps {
        
      }
    }
    stage('Deploy') {
      steps {
        script {
          sh 'docker compose up -d'
        }
      }
    }
  }
}
