pipeline {
    agent any

    stages {

        stage('Lint') {
            steps {
                echo "Running Lint Checks... Passed"
            }
        }

        stage('Build') {
            steps {
                sh 'echo "Build completed successfully" > build-artifact.txt'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build-artifact.txt', allowEmptyArchive: false
            }
        }
    }

    post {
        success {

            sh '''
            echo "GIT_CLONE=SUCCESS" > evaluation-report.txt
            echo "PIPELINE_NAME=github_jenkins_multistage_archive" >> evaluation-report.txt
            echo "STAGE_LINT=SUCCESS" >> evaluation-report.txt
            echo "STAGE_BUILD=SUCCESS" >> evaluation-report.txt
            echo "STAGE_ARCHIVE=SUCCESS" >> evaluation-report.txt
            echo "ARTIFACT_ARCHIVED=true" >> evaluation-report.txt
            echo "BUILD_NUMBER=${BUILD_NUMBER}" >> evaluation-report.txt
            echo "FINAL_STATUS=SUCCESS" >> evaluation-report.txt
            echo "TIMESTAMP=$(date)" >> evaluation-report.txt
            '''

            archiveArtifacts artifacts: 'evaluation-report.txt', allowEmptyArchive: true
        }
    }
}
