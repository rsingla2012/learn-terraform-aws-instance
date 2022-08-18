properties([ parameters([
  string( name: 'AWS_ACCESS_KEY_ID', defaultValue: ''),
  string( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: ''),
  string( name: 'AWS_REGION', defaultValue: ''),
]), pipelineTriggers([]) ])

// Environment Variables.
env.access_key = AWS_ACCESS_KEY_ID
env.secret_key = AWS_SECRET_ACCESS_KEY
env.aws_region = AWS_REGION

/*busybox, alpine*/
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
    /*environment{
        DOCKER_USERNAME = credentials('DOCKER_USERNAME')
        DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')
    }*/
    stages {
        
      
         stage ('Terraform Init'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform init"
          }
       }
         stage ('Terraform Plan'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform plan" 
         }
      }
         stage ('Terraform Apply & Deploy Docker Image on Webserver'){
            steps {
            sh "export TF_VAR_aws_region='${env.aws_region}' && terraform apply -auto-approve"
        }
      }
    }

}


