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
        stage('Creating AWS Launch Template using Packer Image '){
              steps{
		   
			   script{
			       /* AMI_ID = sh ( 
				        script: "aws ec2 describe-images --region ap-south-1 --query 'reverse(sort_by(Images,&CreationDate))[:1].{ImageId:ImageId}' --output text",
				        returnStdout: true).trim()
				   echo "ID : ${AMI_ID}"*/
			   
		     	    	if(params.Select == 'Launch Template'){
			   		sh (
						//script: "aws ec2 create-launch-template --launch-template-name $params.TemplateName --launch-template-data ImageId='${AMI_ID}'"
						script: "aws ec2 create-launch-template --launch-template-name $params.TemplateName --tag-specifications 'ResourceType=launch-template,Tags=[{Key=purpose,Value=production}]'  --launch-template-data ImageId='ami-0da79b55820f19751' "
					)
				}
				else{
					Template_ID = sh(
						aws ec2 describe-launch-templates --filters 'Name=tag:purpose,Values=productio' --query 'LaunchTemplates[].LaunchTemplateId' --output text,
						 returnStdout: true).trim()
					
					echo "Template Id: ${Template_ID}"
					
					sh(
			   			script: "aws ec2 create-launch-template-version --launch-template-id '${Template_ID}' --launch-template-data ImageId='${AMI_ID}'"
					)	
				}  
			   }
                   }
             }
    }
}
