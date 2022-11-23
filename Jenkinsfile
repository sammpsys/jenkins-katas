pipeline {
  agent any
  stages {
    stage('Say Hello') {
      steps {
        sh 'echo "hello world"'
        sh "ls -la ${pwd()}"
        deleteDir()
        sh "ls -la ${pwd()}"
      }
    }

  }
}