pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage('build') {
      steps {
        sh 'docker build -t registry.gmasil.de/docker/gmasil-wiki -f dev/build/Dockerfile .'
      }
    }
    stage('push') {
      steps {
        sh 'docker push registry.gmasil.de/docker/gmasil-wiki:latest'
      }
    }
  }
}
