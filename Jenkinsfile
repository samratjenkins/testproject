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
                sh '''
                echo "Running simple build step"
                #Example test : create a sample report file
                mkdir -p reports
                echo "Build output for commit ${GIT_COMMIT}" > reports/build-report.txt
                echo "Date : $(date)" >> reports/build-report.txt
                '''
            }
        }

        stage('Archive Report'){
            steps{
                archiveArtifacts artifacts: 'reports/**', onlyIfSuccessful: true
            }
        }
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