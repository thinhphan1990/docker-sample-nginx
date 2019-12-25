pipeline {
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/thinhphan1990/docker-sample-nginx.git'
      }
    }
  
    stage('buid') {
      steps {
        echo 'Running build automa'
        sh 'docker build -t test .'
      }
    }

  }
}
