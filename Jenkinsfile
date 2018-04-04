pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        sh 'composer install'
      }
    }
    stage('Test') {
      steps {
        sh './vendor/bin/simple-phpunit'
      }
    }
    stage('Artifact') {
      steps {
        archiveArtifacts(onlyIfSuccessful: true, artifacts: 'release')
      }
    }
  }
  environment {
    APP_ENV = 'dev'
  }
}