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
      parallel {
        stage('Upload Docker Image to Repo') {
          steps {
            withDockerRegistry(credentialsId: 'docker_hub-cred', url: 'https://index.docker.io/v1/') {
              sh "docker push yonibahar/todoapi:${BUILD_ID}"
            }

          }
        }

        stage('Run And Test the Image') {
          steps {
            sh '''docker run -itd -p 80:80 --name todoapi  yonibahar/todoapi:${BUILD_ID};
sleep 3s; curl localhost:80; docker stop todoapi; docker rm todoapi'''
          }
        }

      }
    }

  }
}