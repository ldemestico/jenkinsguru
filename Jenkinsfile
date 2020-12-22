pipeline {
  agent any
  stages {
    stage('repo') {
      parallel {
        stage('repo') {
          steps {
            build 'GitHub Sonar Qube'
          }
        }

        stage('GitHub+Maven+SonarQube') {
          steps {
            build 'com.level3.crm.guru.web'
          }
        }

      }
    }

    stage('docker build') {
      steps {
        sh 'docker build -t level3/crm.guru:2.29.0.0 .'
      }
    }

    stage('holamundo') {
      environment {
        hola = 'chau'
      }
      steps {
        build 'com.level3.crm.guru.web_TEST'
      }
    }

  }
  environment {
    enviroment = 'dev'
  }
}