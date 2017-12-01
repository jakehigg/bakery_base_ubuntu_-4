pipeline {
    agent any 

    stages {
        stage('Git Packer Template') { 
            steps { 
                sh 'rm -rvf bakery_base_ubuntu_14'
                sh 'git clone https://github.com/jakehigg/bakery_base_ubuntu_14.git' 
            }
        }
        stage('Bake') {
            steps {
                withCredentials([string(credentialsId: 'aws_access_key', variable: 'aws_access_key')]) {
                withCredentials([string(credentialsId: 'aws_secret_key', variable: 'aws_secret_key')]) {
                sh '''
                packer build -var "aws_access_key=$aws_access_key" -var "aws_secret_key=$aws_secret_key" -var "source_ami=ami-c29e1cb8" -var "vpc_id=vpc-04bea57d" -var "subnet_id=subnet-86bb84aa" bakery_base_ubuntu_14/packer/bakery.json
                '''
                }}
               
                }
            }
        }
    }

