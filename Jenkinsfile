pipeline {
    agent any
    
    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-cred')
        AWS_SECRET_ACCESS_KEY = credentials('aws-cred')
        AWS_DEFAULT_REGION = 'us-east-1'
    }

    stages {
        stage('Example') {
            steps {
                sh 'aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID'
                sh 'aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY'
                sh 'aws configure set region $AWS_DEFAULT_REGION'
                
                // Now you can run AWS CLI commands or other AWS-related operations
                sh 'aws s3 ls'
                sh 'aws ec2 describe-instances'
            }
        }
        stage('update kubeconfig') {
            steps {
            sh 'aws eks update-kubeconfig --region $AWS_DEFAULT_REGION --name eks'
            sh 'kubectl get nodes'
            sh 'kubectl apply -f /kubernetes/development/nginx.yml'
            }
        }
    }
}
