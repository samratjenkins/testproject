pipeline {

  agent any

  // Run weekly

  triggers { cron('H H * * 0') } // weekly

  stages {

    stage('Checkout') {

      steps {

        checkout scm

      }

    }

    stage('Build') {

      steps {


        bat 'echo Building...'

        bat 'echo Build complete > build-output.txt'

      }

    }

    stage('Test') {

      steps {

        bat 'echo Running tests...'

        // create a tiny test result file to publish (example)

        bat 'echo "<testsuite><testcase classname=\\"sample\\" name=\\"t1\\"/></testsuite>" > test-results.xml'

      }

    }

    stage('Archive') {

      steps {

        archiveArtifacts artifacts: 'build-output.txt', allowEmptyArchive: true

        junit 'test-results.xml' // publishes test results

      }

    }

  }

  post {

    always {

      echo "Pipeline finished"

    }

    success {

      echo "Success"

    }

    failure {

      echo "Failure - investigate"

    }

  }

}
