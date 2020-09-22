pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Build demo-app'
        sh 'sh run_build_script.sh'
      }
    }

    stage('Linux Tests') {
      parallel {
        stage('Linux Tests') {
          steps {
            echo 'Specify Run Linux tests in its configuration panel'
            sh 'sh run_linux_tests.sh'
          }
        }

        stage('Windows Test') {
          steps {
            echo 'specify Run Windows tests in its configuration panel'
          }
        }

      }
    }

    stage('Deploy Staging') {
      steps {
        echo 'Deploy to staging environment '
        input 'Ok to deploy to production'
      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy to Prod'
      }
    }

  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/demoapp.jar', fingerprint: true)
    }

    failure {
      mail(to: 'ci-team@example.com', subject: "Failed Pipeline ${currentBuild.fullDisplayName}", body: " For details about the failure, see ${env.BUILD_URL}")
    }

  }
}