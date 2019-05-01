node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker test'){
     sh 'docker build -t react-test -f Dockerfile.test --no-cache .'
    }
    stage('Docker test'){
      sh 'docker run --rm react-test'
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t Reactjs_22apr --no-cache .'
        sh 'docker tag Reactjs_22apr localhost:5000/Reactjs_22apr'
        sh 'docker push localhost:5000/Reactjs_22apr'
        sh 'docker rmi -f Reactjs_22apr localhost:5000/Reactjs_22apr'
      }
    }
  }
  catch (err) {
    throw err
  }
}
