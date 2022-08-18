pipeline {
  agent {
    kubernetes {
      yaml '''
        apiVersion: v1
        kind: Pod
        spec:
          containers:
          - name: terraform
            image: hashicorp/terraform:latest
            command:
            - cat
            tty: true
        '''
    }
  }
  stages {
      stage ('Terraform Init'){
            steps {
                container('terraform'){
                    sh "terraform --version"
                    sh "terraform init"
                }
          }
       }
      }
  }
