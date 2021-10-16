pipeline {
  agent any
  stages {
    stage('Dev Code Pull') {
      steps {
        echo 'Dev code pull completed'
      }
    }

    stage('Dev Maven Build') {
      steps {
        echo 'Maven Completed'
      }
    }

    stage('QA Deploy') {
      steps {
        echo 'QA To Start'
      }
    }

    stage('QA Test') {
      parallel {
        stage('QA Test') {
          steps {
            echo 'Deploy to QA'
          }
        }

        stage('Web') {
          steps {
            echo 'Code Pull'
            echo 'Run tests'
          }
        }

        stage('API') {
          steps {
            echo 'Code Pull'
            echo 'Run Test'
          }
        }

      }
    }

    stage('QA Certification') {
      steps {
        echo 'UAT Certification'
      }
    }

    stage('UAT Deploy') {
      steps {
        echo 'UAT Deploy'
      }
    }

    stage('UAT Certification') {
      steps {
        echo 'UAT Certification'
      }
    }

  }
}