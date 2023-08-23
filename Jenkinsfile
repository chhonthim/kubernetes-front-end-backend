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

    stage('Build image') {
      steps{
        script {
          //dockerImage = docker.build dockerimagename
          sh '/var/lib/jenkins/workspace/ernetes-front-end-backend_master/build_and_push_docker.sh'
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
