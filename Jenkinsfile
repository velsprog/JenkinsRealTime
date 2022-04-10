pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/velsprog/WebApp.git', branch: 'master', poll: true)
        script {
          script {
            try {
              bat "start /min StopApp.bat"
            }catch(Exception e) {
              echo "No PID is running"
            }
          }
        }

        bat 'mvn install'
        bat 'StartApp.bat'
      }
    }

  }
}