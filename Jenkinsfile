pipeline {
  agent any
  

  stages {
    stage('docker build') {
      steps {
        sh 'docker build -t level3/crm.guru:2.29.0.0 .'
      }
    }

    stage('DockerPush') {
      steps {
        sh 'docker push ardl-dockerhub01:5000/level3/crm.guru:2.29.0.0'
      }
    }

    stage('Deploy Kubernetes') {
      steps {
        build 'com.level3.crm.guru.web_dockerregistry'
      }
    }

  }
  environment {
    enviroment = 'dev'
  }
}
