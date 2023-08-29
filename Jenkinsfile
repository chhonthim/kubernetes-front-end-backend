pipeline {

  environment {
    dockerimagename = "bravinwasike/react-app"
    dockerImage = ""
  }

  agent master1

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/chhonthim/kubernetes-front-end-backend.git'
      }
    }

    stage('Build image Fronend') {
      steps{
        script {
            // Build Docker image with custom options
            sh "docker buildx build -t thimchhon/k8app-frontend-image -f .frontend/frontend.dockerfile"
        }
      }
    }

  }

}
