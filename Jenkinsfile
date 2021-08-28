pipeline {
  agent {
    node {
      label 'docker-vm'
    }

  }
  stages {
    stage('Chekout Code') {
      steps {
        git(url: 'https://github.com/yonibahar/dotnet-core-api.git', branch: 'master', changelog: true, poll: true)
      }
    }

    stage('Build Image of Docker') {
      steps {
        sh 'docker build -t yonibahar/todoapi:${BUILD_ID} .'
      }
    }

    stage('Upload Docker Image to Repo') {
      steps {
        echo 'Hello'
      }
    }

  }
}