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
        sh 'rm -rf var/cache/*'
        sh 'APP_ENV=prod /usr/local/bin/composer install --prefer-dist --no-dev --optimize-autoloader --no-interaction'
        sh 'mkdir /tmp/release'
        sh 'cp -r * /tmp/release/'
        sh 'tar --exclude="*.git" -zcf release.tgz /tmp/release/*'
        sh 'rm -rf /tmp/release'
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