pipeline {
  agent any
  stages {
    stage('dev-git-pull') {
      steps {
        git 'https://github.com/ramesh610/WebAppNew.git'
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
              customWorkspace 'workspace/WebAppUIAutomation1'
              label 'master'
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
              customWorkspace 'workspace/WebAppAPIAutomation1'
              label 'master'
            }

          }
          steps {
            git 'https://github.com/ramesh610/WebAppApiAutomation.git'
            bat 'mvn test'
          }
        }

      }
    }

    stage('Deploy to UAt') {
      steps {
        echo 'echo \'Deploy to UAT (AWS)\''
        echo 'echo \'Notify the UAT users\''
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