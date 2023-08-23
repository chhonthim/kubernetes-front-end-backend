pipeline {

  environment {
    dockerimagename = "bravinwasike/react-app"
    dockerImage = ""
  }

  agent any

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
            sh "docker buildx build -t thimchhon/k8app-frontend-image -f /var/lib/jenkins/workspace/ernetes-front-end-backend_master/frontend/frontend.dockerfile ."
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credential'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
            dockerImage.push("latest")
          }
        }
      }
    }

  }

}
