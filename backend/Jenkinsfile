pipeline {
  agent any
  stages {
    estage ('Build') {
      steps{
        sh 'printenv'
      }
    }
    stage ('Publish ECR') {
      steps {
        withEnv (["AWS_ACESS_KEY_ID=$(env.AWS_ACESS_KEY_ID)", "AWS_SECRET_ACESS_KEY=$(env.AWS_SECRET_ACESS_KEY)", "AWS_DEFAULT_REGION=$(env.AWS_DEFAULT_REGION)"]) {
          sh 'docker login -u AWS -p $(aws ecr-public get-login-password --region us-east-1) public.ecr.aws/j0v2f3y8'
          sh 'docker build -t ecr-demo-img .'
          sh 'docker build tag ecr-demo-img: ""$BUILD_ID""'
          sh 'docker push public.ecr.aws/j0v2f3y8/ecr-demo-img:""$BUILD_ID""'
        }
      }
    }
  }
}
