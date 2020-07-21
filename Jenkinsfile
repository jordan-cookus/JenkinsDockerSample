pipeline {

  environment {
    registry = "jordansandhills/cheers2019"
    registryCredential = 'bb4bede9-21ea-44b6-bb63-b71d0dd0dfa5'
    devRemoteCredentials = credentials('sigpudev1')
    dockerImage = ''
  }

  parameters{
    string(name: 'TOID', defaultValue: '', description:'Rollout TOID if applicable')
  }

  agent {
    label 'slave_sigpudev1'
  }

  stages {

      stage('Initialize'){
          steps{
            buildName "#$BUILD_NUMBER ${params.TOID}"
            buildDescription "Executed @ ${NODE_NAME}"
          }
      }

    //   stage('Test stage'){
    //       agent {
    //         label 'slave_sigpudev1'
    //       }
    //       steps{
    //         echo 'test'   
    //         sh "hostname"
    //       }
    //   }

    stage('Cloning Git') {
      steps {
        git 'https://github.com/jordan-cookus/JenkinsDockerSample.git' // this pulls all files into ~\Jenkins\workspace\pipline
      }
    }

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
          echo ":$BUILD_NUMBER"
        }
      }
    }

    // stage('Run Remote Script'){
    //     steps{
    //         script{
    //             def remote = [:]
    //             remote.name = 'test'
    //             remote.host = 'sigpudev1'
    //             remote.user = devRemoteCredentials_USR
    //             remote.password = devRemoteCredentials_PSW
    //             remote.allowAnyHosts = true
    //             sshScript remote: remote, script: "script.sh" //local machine directory 
    //         }
    //     }
    // }
    
    stage('Run build script'){
      steps{
        sh 'bash script.sh'
        // echo 'teststage'               
      }
    }
    
    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
