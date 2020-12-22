pipeline {
  agent any
  stages {
    stage('Docker Build and Test SonarQube') {
      steps {
        build 'com.level3.crm.guru.web'
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push ardl-dockerhub01:5000/level3/crm.guru:2.29.0.0'
      }
    }

    stage('Deploy Kubernetes') {
      steps {
        build 'com.level3.crm.guru.web_dockerregistry'
      }
    }

    stage('Check Pods') {
      steps {
        build(job: 'com.level3.crm.guru.web_checkpod', wait: true, quietPeriod: 19)
      }
    }

  }
  environment {
    ambiente = 'dev'
    tag = '2.29.0.0'
    ss = 'aa'
  }
}