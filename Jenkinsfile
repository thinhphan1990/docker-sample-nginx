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
         stage('push image') {
       steps 
       {
         script {
                   sh 'rm  ~/.dockercfg || true'
                  sh 'rm ~/.docker/config.json || true'                    
           
                    docker.withRegistry('https://076218049049.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:bttrm-backend-ecr') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
         }
       }
     }
  }
}
