pipeline {

  agent { label 'stage'}

  tool {
    jdk 'java11'
    maven 'Maven3'
  }

  environments{

    APP_NAME = "register-app-pipeline"
    RELEASE= "1.0.0"
    DOCKER_USER= "ajaykumara"
    DOCKER_PASS = 'dockerhub'
    IMAGE_NAME= "${DOCKER_USER}" + "/" + "${APP_NAME}"
    IMAGE_TAG= "${RELEASE}-${BUILD_NUMBER}"
  }

  stages {
    stage("Cleanup Workspace"){
      steps{
        cleanWs()
      }
    }

    stage("Checkout from SCM"){
      steps{
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/ajaykumarbk/imdbClone.git'
      }
    }

    stage("Build application"){
      steps{
       sh 'mvn clean package'
      }
    }

    stage("Test application"){
      steps{
       sh 'mvn test'
      }
    }

     stage("Build and push Docker Image"){
      steps{
       scripts{
        docker.withRegistry('',DOCKER_PASS){
            docker_image = docker.build "${IMAGE_NAME}"
        }

        docker.withRegistry('',DOCKER_PASS){
           docker_image.push ("${IMAGE_TAG}")
           docker.docker_image ('latest')

        }

       }
      }
    }
  }
}
