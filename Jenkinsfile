pipeline {
  agent any
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

        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min StartApp.bat'
      }
    }

    stage('UI-Automation') {
      steps {
        git(url: 'https://github.com/velsprog/WebAppUiAutomation.git', branch: 'master', poll: true)
        sleep 10
        bat 'mvn test'
      }
    }

  }
  tools {
    maven 'MAVEN_HOME'
    jdk 'JAVA_HOME'
  }
}