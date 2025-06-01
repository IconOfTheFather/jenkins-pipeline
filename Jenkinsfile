pipeline {
    agent any

    environment{
     AWS_REGION = 'us-east-1'
     ECR_REPO = '590184023519.dkr.ecr.us-east-1.amazonaws.com/devops'
     IMAGE_TAG = '590184023519.dkr.ecr.us-east-1.amazonaws.com'

    }

    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
                

            }
        }
    stage('dockerLogin'){
        steps{
            sh "aws ecr get-login-password --region $AWS_REGION |\
             docker login --username AWS \
              --password-stdin $ECR_REGION"
        }
    }    
    stage('dockerImageBuild') {
        steps{
            sh 'docker build -t devops .'
            sh 'docker build -t imageversion .' 
        } 
}
    stage('dockerImageTag'){
        steps{
            sh "docker tag devops:latest\
             $ECR_REPO:latest"
            sh "docker tag imageversion \
             $ECR_REPO:v1.$BUILD_NUMBER"
        }
    }
    stage('pushImage'){
        steps{
            sh "docker push \
            $ECR_REPO:latest"
            sh "docker push \
            $ECR_REPO:v1.$BUILD_NUMBER"
        }
    }      
    }
}