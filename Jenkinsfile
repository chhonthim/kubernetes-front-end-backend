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
          sh '''
                        #!/bin/bash
                        if [[ $# -ne 1 || $1 != "backend" && $1 != "frontend" ]]; then
                            echo "Script takes one argument which must be either 'backend' or 'frontend'. Value given: '$1'"
                            exit 1
                        fi

                        echo "Running docker pipeline for: $1"
                        echo ""

                        echo "Building container"
                        build_command="docker build $1 -f $1/$1.dockerfile -t thimchhon/k8app-$1-image"
                        echo -e "\t$build_command"
                        eval $build_command
                        echo ""

                        echo "Pushing container"
                        push_command="docker push thimchhon/k8app-$1-image"
                        echo -e "\t$push_command"
                        eval $push_command
                        echo ""
                    '''
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
