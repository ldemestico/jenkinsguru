pipeline {
  agent any
def remote = [:]
remote.name = "masterk8"
remote.host = "10.48.41.11"
remote.allowAnyHosts = true
        remote.user = 'root'
        remote.password = 'level3'
  
  stages {
    stage('repo') {
      steps {
        build 'GitHub Sonar Qube'
      }
    }

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
 stage('apply development') {
   steps {
        // Run the maven build
sshCommand remote: remote, command: 'kubectl apply -f /root/deployment-guruweb.yaml'
    }
        }

  }
  environment {
    enviroment = 'dev'
  }
}
