pipeline {

  agent { label 'stage' }

  tools {
    jdk 'java11'
    maven 'Maven3'
  }

  environment {
    APP_NAME     = "register-app-pipeline"
    RELEASE      = "1.0.0"
    DOCKER_USER  = "ajaykumara"
    IMAGE_NAME   = "${DOCKER_USER}/${APP_NAME}"
    IMAGE_TAG    = "${RELEASE}-${BUILD_NUMBER}"
  }

  stages {

    stage("Cleanup Workspace") {
      steps {
        cleanWs()
      }
    }

    stage("Checkout from SCM") {
      steps {
        git branch: 'main', credentialsId: 'github', url: 'https://github.com/ajaykumarbk/imdbClone.git'
      }
    }

    stage("Build application") {
      steps {
        sh 'mvn clean package'
      }
    }

    stage("Test application") {
      steps {
        sh 'mvn test'
      }
    }

    stage("Build and Push Docker Image") {
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
            def dockerImage = docker.build("${IMAGE_NAME}:${IMAGE_TAG}")
            dockerImage.push()
            dockerImage.push("latest")
          }
        }
      }
    }
  }

  post {
    always {
      cleanWs()
    }
  }
}
