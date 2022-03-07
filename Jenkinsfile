pipeline{   
    agent any
    stages{
        stage('Checkout external proj') {
            steps {
		    script{
                git branch: 'main',
                    credentialsId: 'fjenkins', 
                    url: 'git@github.com:fmerchant31/AWSPacker.git'
		    }}
        }
        stage('Creating AWS Launch Template using Packer Image'){
              steps{
		   withAWS(credentials:'aws-credentials'){
			   script{
			        AMI_ID = sh ( 
				        script: "aws ec2 describe-images --region ap-south-1 --query 'reverse(sort_by(Images,&CreationDate))[:1].{ImageId:ImageId}' --output text",
				        returnStdout: true).trim()
				   echo "ID : ${AMI_ID}"
			      }
		   }
                   }
             }
    }
}
