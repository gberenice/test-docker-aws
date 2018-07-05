node {
  stage 'Checkout'
  git 'https://github.com/gberenice/test-docker-aws.git'
 
  stage 'Docker build'
  docker.build('test-repo')
 
  stage 'Docker push'
  docker.withRegistry('https://<account_id_must_be_here>.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-1:demo-ecr-credentials') {
    docker.image('test-repo').push('latest')
  }
  
  stage 'Beanstalk'
  step([$class: 'AWSEBDeploymentBuilder', applicationName: 'test-app', awsRegion: 'us-east-2', bucketName: '', checkHealth: true, credentialId: 'demo-ecr-credentials', environmentName: 'testApp-env', excludes: '', includes: '', keyPrefix: '', maxAttempts: 30, rootObject: 'Dockerrun.aws.json', sleepTime: 90, versionDescriptionFormat: 'latest', versionLabelFormat: 'latest', zeroDowntime: false])
}
