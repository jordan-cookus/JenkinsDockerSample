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
        sshScript 'script.sh'
      }
    }

    stage('error') {
      steps {
        sshScript 'script.sh'
      }
    }

  }
}