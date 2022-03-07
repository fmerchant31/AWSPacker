pipeline{   
    agent any
    stages{
        stage('Checkout external proj') {
            steps {
                git branch: 'master',
                    credentialsId: 'f845af59-d281-4b2d-9170-2eca1a1a0b63', 
                    url: 'git@github.com:fmerchant31/AWSPacker.git'
            }
        }
    }
}
