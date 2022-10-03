pipeline {
agent any

stages{
  stage('Terraform Init'){
    steps {
	    dir('./gitops') {
                       sh '/usr/local/bin/terraform init'
        }
    }
  }
  stage('Terraform Plan'){
    steps {
	    dir('./gitops') {
                       sh '/usr/local/bin/terraform plan'
        }
    }
  }
  stage('Approval'){
    when { branch 'main'}
    steps {
      script {
         waitUntil {
           fileExists('dummyfile')
         }
      }
    }
  }
  stage('Terraform Apply'){
    steps {
	    dir('./gitops') {
                       sh '/usr/local/bin/terraform apply -auto-approve'
        }
    }
  }
}
}
