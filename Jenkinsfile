pipeline{   
    agent any
    stages{
        stage('Checkout external proj') {
            steps {
                git branch: 'main',
                    credentialsId: 'f845af59-d281-4b2d-9170-2eca1a1a0b63', 
                    url: 'git@github.com:fmerchant31/AWSPacker.git'
            }
        }
        stage('Creating AWS Launch Template using Packer Image'){
              steps{
                   
			   withAWS(credentials:'aws-credentials'){
			        AMI_ID = sh ( 
				        script: "aws ec2 describe-images --region ap-south-1 --query 'reverse(sort_by(Images,&CreationDate))[:1].{ImageId:ImageId}' --output text",
				        returnStdout: true).trim()
				   echo "ID : ${AMI_ID}"}
                   }
                   }
    }
}
