pipeline {
  agent {
    node {
      label 'docker-vm'
    }

  }
  stages {
    stage('chekout code') {
      steps {
        git(url: 'https://github.com/yonibahar/dotnet-core-api.git', branch: 'master', changelog: true, poll: true)
      }
    }

  }
}