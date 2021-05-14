pipeline {
    agent { label 'ec2-aws'}
    
    tools {
        terraform 'terraform'
    }
    
    stages {
      
        stage('Git checkout') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/Kristin0/epam-training-terraform'
            }
        }
        
        stage('Terraform init') {
            environment {
            AWS_ACCESS_KEYS = credentials('ssh-aws-keys')
        }
            steps {
                sh 'terraform init'
                
            }
            
        }
          
        stage('Terraform apply') {
            environment {
            AWS_ACCESS_KEYS = credentials('ssh-aws-keys')
        }
            steps {
                sh 'terraform apply --auto-approve'
                
            }
            
        }
        
        stage('Ansible') {
            steps {
                sh 'sudo amazon-linux-extras install ansible2 -y'
                sh 'cd ansible/ && ansible-playbook wordpress.yml -i inventory'
                
            }
        }
    }
}
