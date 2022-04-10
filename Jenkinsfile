pipeline {
  agent any
  maven 'MAVEN_HOME'
  jdk 'JAVA_HOME'
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/velsprog/WebApp.git', branch: 'master', poll: true)
        bat 'mvn install'
        script {
            try {
              bat "start /min StopApp.bat"
            }catch(Exception e) {
              echo "No PID is running"
            }
        }

        bat 'StartApp.bat'
      }
    }

  }
}
