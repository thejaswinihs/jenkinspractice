pipeline{
    agent {label 'appserver'}
    stages{
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/thejaswinihs/jenkinspractice.git']]])
            }
        }
        stage('build and push image to ecr'){
            steps{
                sh '''docker build -t sgecr .
                docker tag sgecr:latest public.ecr.aws/e4v8g7r7/appupgrad
                docker push public.ecr.aws/e4v8g7r7/appupgrad'''
            }
        }
        stage('run container'){
            steps{
                sh '''docker run -d -p 8080:8080 public.ecr.aws/e4v8g7r7/appupgrad'''
            }
        }
}
}



