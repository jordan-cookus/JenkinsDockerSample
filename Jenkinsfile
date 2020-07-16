pipeline {
  agent any
  stages {
    stage('stage') {
      steps {
        git 'https://github.com/jordan-cookus/JenkinsDockerSample.git'
      }
    }

    stage('stage2') {
      steps {
        sh '''dockerImage = docker.build registry + ":$BUILD_NUMBER"
          echo ":$BUILD_NUMBER"'''
      }
    }

    stage('error') {
      steps {
        sh '''docker.withRegistry( \'\', registryCredential ) {
            dockerImage.push()'''
        }
      }

    }
  }