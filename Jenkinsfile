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
        sh 'docker build -t level3/crm.guru:2.29.0.0 /home/l3docker.dev/com.level3.crm.guru.web/'
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
  }
}