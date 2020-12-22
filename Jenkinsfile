pipeline {
  agent any
  stages {
    stage('SonarQube') {
      steps {
        build 'com.level3.crm.guru.web'
      }
    }

    stage('Build Docker') {
      steps {
        sh '''cd /home/l3docker.dev/.jenkins/jobs/com.level3.crm.guru.web









; docker build -t level3/crm.guru:2.29.0.0 .'''
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

  }
  environment {
    ambiente = 'dev'
    tag = '2.29.0.0'
  }
}