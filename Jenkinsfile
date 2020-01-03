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
        def remote = [:]
        remote.name = "node-1"
        remote.host = "192.168.0.16"
        remote.allowAnyHosts = true

       steps 
       {
          withCredentials([sshUserPrivateKey(credentialsId: 'sshUser', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                  remote.user = userName
                  remote.identityFile = identity
                  stage("SSH Steps Rocks!") {
                      writeFile file: 'abc.sh', text: 'ls'
                      sshCommand remote: remote, command: 'for i in {1..5}; do echo -n \"Loop \$i \"; date ; sleep 1; done'
                      sshPut remote: remote, from: 'abc.sh', into: '.'
                      sshGet remote: remote, from: 'abc.sh', into: 'bac.sh', override: true
                      sshScript remote: remote, script: 'abc.sh'
                      sshRemove remote: remote, path: 'abc.sh'
                  }
          }
       }
     }
  }
}
