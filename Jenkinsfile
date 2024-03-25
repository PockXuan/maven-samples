pipeline {
  agent any
  tools { 
      maven 'DHT_MVN' 
      jdk 'DHT_SENSE' 
  }
  stages {
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

