pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/thinhphan1990/docker-sample-nginx.git'
      }
    }
    stage('Initialize'){
        def dockerHome = tool 'myDocker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
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
