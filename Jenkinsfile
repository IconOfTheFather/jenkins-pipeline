pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
                

            }
        }
    stage('dockerLogin'){
        steps{
            sh 'aws ecr get-login-password --region us-east-1 |\
             docker login --username AWS \
              --password-stdin 590184023519.dkr.ecr.us-east-1.amazonaws.com'
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
            sh 'docker tag devops:latest\
             590184023519.dkr.ecr.us-east-1.amazonaws.com/devops:latest'
            sh 'docker tag imageversion \
             590184023519.dkr.ecr.us-east-1.amazonaws.comdevops:v1.$BUILD_NUMBER'
        }
    }
    stage('pushImage'){
        steps{
            sh 'docker push 590184023519.dkr.ecr.us-east-1.amazonaws.com/devops:latest'
            sh 'docker push 590184023519.dkr.ecr.us-east-1.amazonaws.com/devops:v1.$BUILD_NUMBER'
        }
    }      
    }
}