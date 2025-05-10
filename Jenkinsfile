pipeline {

  agent { label 'stage'}

  tool {
    jdk 'java11'
    maven 'Maven3'
  }

  stages {
    stage("Cleanup Workspace"){
      steps{
        cleanWs()
      }
    }
  
    
  }
}
