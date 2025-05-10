pipeline {

  agent { label 'stage' }

  tools {
    jdk 'Java11'
    maven 'Maven3'
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
  }
}
