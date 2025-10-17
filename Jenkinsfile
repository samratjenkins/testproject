pipeline{
    agent any

    triggers {
    // run every 7 days
    cron('H H * * 0')
    }

    stages{
        stage('Checkout'){
            steps{
                checkout scm
                echo "Checking out ${env.GIT_COMMIT}"
            }
        }

        stage('Build / Test ( example )'){
            steps{
                bat '''
                echo "Running simple build step"
                #Example test : create a sample report file
                md reports
                echo "Build output for commit ${GIT_COMMIT}" > reports/build-report.txt
                echo "Date : $(date)" >> reports/build-report.txt
                '''
            }
        }

        stage('Generate HTML report') {

          steps {

            bat '''

              md reports/html

              echo "<html><body><h1>Report</h1><p>Commit ${GIT_COMMIT}</p></body></html>" > reports/html/index.html

            '''

          }

        }

        stage('Archive and publish HTML') {

          steps {

            archiveArtifacts artifacts: 'reports/**'

            publishHTML([allowMissing: false, alwaysLinkToLastBuild: true, keepAll: true, reportDir: 'reports/html', reportFiles: 'index.html', reportName: 'Simple HTML Report'])

          }

        }

        /*
        stage('Archive and publish HTML Report'){
            steps{
                archiveArtifacts artifacts: 'reports/**', onlyIfSuccessful: true
            }
        }
        */
    }

    post{
        success{
            echo "Pipeline succeeded"
        }
        failure{
            echo "Pipeline failed - check console output"
        }
    }





}