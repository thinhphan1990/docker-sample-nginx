
pipeline {
  agent any
  environment {
    PATH = "/usr/local/bin:$PATH"
    TAG = "latest"
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
                   sh '$(aws ecr get-login --no-include-email --region ap-southeast-1)'

           sh 'docker tag test:latest 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest'
           sh 'docker push 076218049049.dkr.ecr.ap-southeast-1.amazonaws.com/test:latest'
         }
       }
     }
    stage('ssh-test') {
       steps 
       {
          withCredentials([sshUserPrivateKey(credentialsId: "SshToSever-test", keyFileVariable: 'keyfile')]) {

              sh "ssh -i ${keyfile} -o StrictHostKeyChecking=no root@192.168.0.16 \"/tmp/dxs-o2o-backend/ecr-login.sh\" \"TAG=${TAG}\" \"/usr/local/bin/docker-compose -f  /tmp/dxs-o2o-backend/docker-compose.yml -f  /tmp/dxs-o2o-backend/docker-compose.dev.yml up -d\""
             
        }
       }
     }
  }
}
