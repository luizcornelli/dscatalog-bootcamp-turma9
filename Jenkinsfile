pipeline {
  agent any
  stages {
    stage ('Build') {
      steps{
        sh 'printenv'
      }
    }
    stage ('Publish ECR') {
      steps {
        withEnv (["AWS_ACCESS_KEY_ID=${env.AWS_ACCESS_KEY_ID}", "AWS_SECRET_ACCESS_KEY=${env.AWS_SECRET_ACCESS_KEY}", "AWS_DEFAULT_REGION=${env.AWS_DEFAULT_REGION}"]) {
          sh 'aws ecr-public get-login-password --region us-east-1 | docker login --username AWS --password-stdin public.ecr.aws/j0v2f3y8'
          sh 'docker build -t ecr-demo-img .'
          sh 'docker tag ecr-demo-img:latest public.ecr.aws/j0v2f3y8/ecr-demo-img:""$BUILD_ID""'
          sh 'docker push public.ecr.aws/j0v2f3y8/ecr-demo-img:""$BUILD_ID""'
        }
      }
    }
  }
}
