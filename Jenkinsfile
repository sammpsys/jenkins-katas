pipeline {
  agent any
  stages {
        stage('clone down') {
            agent {
                label 'master-label'
            }
            steps{
                stash excludes: '.git/', name: 'code'
            }
    }
    stage('Parallel execution') {
      parallel {
        stage('Say Hello') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('build app') {
          options {
            skipDefaultCheckout(true)
          }
          steps {
              unstash 'code'
          }
        }
        stage('test app') {
            agent {
                docker {
                    image 'gradle:6-jdk11'
                }
            }
            steps {
                unstash 'code'
                sh './ci/unit-test-app.sh'
                junit 'app/build/test-results/test/TEST-*.xml'
            }
        }
        }
    }

  }
  post {
    cleanup {
        deleteDir() /* clean up our workspace */
    }
  }
}