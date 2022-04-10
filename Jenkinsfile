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
                          agent {
                        label {
                            label 'Jenkins_Slave'
                            //It will create separate workspace for QA, instead of override the dev workspace
                            customWorkspace 'workspace/WebAppUiAutomation'
                        }
                    }
      steps {
        git(url: 'https://github.com/velsprog/WebAppUiAutomation.git', branch: 'master', poll: true)
        sleep 5
        bat 'mvn test'
      }
    }

  }
  tools {
    maven 'MAVEN_HOME'
    jdk 'JAVA_HOME'
  }
}
