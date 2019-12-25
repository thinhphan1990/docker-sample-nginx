pipeline {
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/thinhphan1990/docker-sample-nginx.git'
      }
    }
     stage('Build image') {
       steps 
       {
        sh 'docker build -t test:latest .'
       }
     }
  }
}
