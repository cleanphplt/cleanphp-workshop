pipeline {
  agent any
  stages {
    stage('Prepare') {
      steps {
        sh '/usr/local/bin/composer install  --prefer-dist --optimize-autoloader --no-interaction'
      }
    }
    stage('Test') {
      steps {
        sh 'vendor/bin/simple-phpunit'
      }
    }
    stage('Create release version') {
      steps {
        sh '/usr/local/bin/composer install --prefer-dist --no-dev --optimize-autoloader --no-interaction'
        sh 'tar --exclude="*.git" -zcf release.tgz .'
      }
    }
    stage('Artifact') {
      steps {
        archiveArtifacts(onlyIfSuccessful: true, artifacts: 'release.tgz')
      }
    }
  }
  environment {
    APP_ENV = 'dev'
  }
}