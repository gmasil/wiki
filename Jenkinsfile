pipeline {
  agent {
    label 'linux'
  }
  stages {
    stage('build') {
      steps {
        retry(count: 3) {
          sh 'docker build -t registry.gmasil.de/docker/gmasil-wiki -f dev/build/Dockerfile .'
        }
      }
    }
    stage('push') {
      environment {
        DOCKER_USERNAME = credentials('DOCKER_USERNAME')
        DOCKER_PASSWORD = credentials('DOCKER_PASSWORD')
      }
      steps {
        sh 'echo ' + env.DOCKER_PASSWORD + ' | docker login -u ' + env.DOCKER_USERNAME + ' --password-stdin registry.gmasil.de'
        sh 'docker push registry.gmasil.de/docker/gmasil-wiki:latest'
      }
    }
    stage('deploy') {
      steps {
        sh 'docker restart wikijs'
      }
    }
  }
}
