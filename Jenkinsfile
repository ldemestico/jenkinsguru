pipeline {
  agent any
  stages {
    stage('repo') {
      steps {
        git(url: 'https://github.com/CenturyLink/GURU-com.level3.crm.guru.web.git', branch: 'master', poll: true, changelog: true, credentialsId: 'testluc')
      }
    }

    stage('docker build') {
      steps {
        sh 'docker build -t level3/crm.guru:2.29.0.0 .'
      }
    }

  }
  environment {
    enviroment = 'dev'
  }
}