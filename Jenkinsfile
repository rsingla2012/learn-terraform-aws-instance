pipeline {
  agent {
    kubernetes {
      //cloud 'kubernetes'
      yaml """
        apiVersion: v1
        kind: Pod
        metadata:
        name: kaniko
        spec:
        containers:
        - name: slave-pod
            image: jenkins/inbound-agent
            imagePullPolicy: Always
        """
    }
  }
  stages {
      stage('build') {
          steps {
            
                sh 'apt-get update'
                sh 'apt-get install -y gnupg software-properties-common curl' 
                sh 'curl -fsSL https://apt.releases.hashicorp.com/gpg |  apt-key add - '
                sh 'apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main" '
                sh 'apt-get update' 
                sh 'apt-get install terraform'
            }
              
          }
      }
  }
