pipeline {
  agent any
  tools {
    maven '3.9.6'
    jdk 'Java 8'
  }
  stages {
    stage('checkout') {
      steps {
        git(url: 'https://github.com/PockXuan/maven-samples', branch: 'master')
      }
    }

    stage('run') {
      steps {
        sh 'mvn verify'
      }
    }

  }
}
