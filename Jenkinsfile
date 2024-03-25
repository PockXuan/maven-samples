pipeline {
  agent any
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

    stage('test') {
      steps {
        sh 'mvn test'
      }
    }

    stage('verify') {
      steps {
        sh 'mvn verify'
      }
    }

    stage('clean') {
      steps {
        sh 'mvn clean'
      }
    }

    stage('Find Bug-Introducing Commit') {
        steps {
            script {
                // Initialize environment variables for the known good and bad commits
                env.GOOD_COMMIT = 'hash_of_good_commit'
                env.BAD_COMMIT = 'hash_of_bad_commit'

                // Bisect process script
                sh '''
                git bisect start
                git bisect bad $BAD_COMMIT
                git bisect good $GOOD_COMMIT
                git bisect run mvn clean test
                '''
            }
        }
    }
    
  }
  post {
      always {
          script {
              // Cleanup: make sure to end the bisect session after the job, even if it fails
              sh 'git bisect reset'
          }
      }
  }

}

