
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
        sh '$(aws ecr get-login --no-include-email --region ap-southeast-1)'
           sh 'docker build -t test .'


         }
       }
     }
         stage('push image') {
       steps 
       {
         script {
                   sh 'rm  ~/.dockercfg || true'
                  sh 'rm ~/.docker/config.json || true'                    
           
           sh 'docker tag test:latest 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest'
            sh 'docker push 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest'

         }
       }
     }
    stage('ssh-test') {
       steps 
       {
          withCredentials([sshUserPrivateKey(credentialsId: "SshToSever-test", keyFileVariable: 'keyfile')]) {
              
              sh "ssh -i ${keyfile} -o StrictHostKeyChecking=no root@192.168.0.16 \"/usr/local/bin docker pull redis\""
             
        }
                  

       }
     }
  }
}
