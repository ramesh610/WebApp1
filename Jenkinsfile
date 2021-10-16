pipeline {
  agent any
  stages {
    stage('dev-git-pull') {
      steps {
        git 'https://github.com/TestLeafInc/WebApp.git'
      }
    }

    stage('dev-build') {
      steps {
        bat 'start /min StopApp.bat'
        bat 'mvn install'
        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min StartApp.bat'
      }
    }

    stage('Testing') {
      parallel {
        stage('qa-git-ui-test') {
          agent {
            node {
              customWorkspace 'workspace/WebAppUIAutomation'
              label '\' \''
            }

          }
          steps {
            git 'https://github.com/ramesh610/WebAppUiAutomation.git'
            sleep(time: 10, unit: 'SECONDS')
            bat 'mvn test'
          }
        }

        stage('qa-git-api-test') {
          agent {
            node {
              customWorkspace 'workspace/WebAppAPIAutomation'
              label '\' \''
            }

          }
          steps {
            git 'https://github.com/ramesh610/WebAppApiAutomation.git'
            bat 'mvn test'
          }
        }

      }
    }

  }
  tools {
    maven 'Maven'
  }
  post {
    always {
      echo 'Either success or failure'
    }

    success {
      echo 'send mail to my pm'
    }

    failure {
      echo 'sent it to dev'
    }

  }
  triggers {
    cron('50 14 * * 0')
  }
}