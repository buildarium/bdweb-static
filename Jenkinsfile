pipeline {
  environment {
    registry = "buildarium/bdweb-static"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }

  agent any

  stages {
    stage('Test') {
      steps {
        git 'https://github.com/buildarium/bdweb-static.git'
      }
    }
    stage('Build') {
      steps {
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploy') {
      steps{
        script {
          docker.withRegistry('', registryCredential) {
            dockerImage.push()
          }
        }
        sh "docker rmi $registry:$BUILD_NUMBER"
      }
    }
  }
}