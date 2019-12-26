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
          sh "docker build -t 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest  ."

         }
       }
     }
         stage('push image') {
       steps 
       {
         script {
              docker.withRegistry('076218049049.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:bttrm-backend-ecr') {
              sh "docker push 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest"
        }
         }
       }
     }
  }
}
