node {
  stage 'Checkout'
  git 'https://github.com/irwin-tech/docker-pipeline-demo.git'
 
  stage 'Docker build'
  docker.build('test-repo')
 
  stage 'Docker push'
  docker.withRegistry('https://642215596270.dkr.ecr.us-east-2.amazonaws.com', 'ecr:us-east-1:demo-ecr-credentials') {
    docker.image('test-repo').push('latest')
  }
}