pipeline {
  agent any
    environment {
    PATH = "/usr/local/bin:$PATH"
  }
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/thinhphan1990/docker-sample-nginx.git'
      }
    }
     stage('Build image') {
       steps 
       {
         script {
          app = docker.build("test")
         }
       }
     }
  }
}
