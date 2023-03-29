pipeline{

 agent any
 stages {
    stage('init') {
    steps {
        sh 'terraform init'
    }
    }
    stage('plan') {
    steps {
        withCredentials([aws(accessKeyVariable:'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVarible: 'AWS_SECRET_ACCESS_KEY')]) {
        sh 'terraform plan '
        }
    }
    }
    stage('terraform apply') {
    steps {
        
        s([aws(accessKeyVariable:'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVarible: 'AWS_SECRET_ACCESS_KEY')]) {
        sh 'terraform apply  -auto-approve '
        }
    }
    }
    stage('terraform destroy') {
    input {
    message 'Please select environment'
    id 'envId'
    ok 'Submit'
    submitterParameter 'approverId'
    parameters {
        choice choices: ['es', 'No'], name: 'envType'
    }
    }
    steps {
        withCredentials([aws(accessKeyVariable:'AWS_ACCESS_KEY_ID', credentialsId: 'aws', secretKeyVarible: 'AWS_SECRET_ACCESS_KEY')]) {
        sh 'terraform destroy -auto-approve '
        }
    }
    }
 }
}
  