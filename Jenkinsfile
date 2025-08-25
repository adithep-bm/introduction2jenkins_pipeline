pipeline {
    agent any
    // parameters {
         // booleanParam(name: 'RUN_DEPLOY', defaultValue: false, 
         // description: 'Should we deploy?')
    // }
    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
                // sh 'exit 1'
            }
        }
        stage('Test in Parallel') {
            parallel{
                stage('Unit Tests') {
                    // when {
                    //     expression { currentBuild.currentResult == 'SUCCESS' }
                    // }
                    steps {
                        echo 'Running unit tests...'
                        sh 'sleep 5'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        echo 'Running integration tests...'
                        sh 'sleep 5'
                    }
                }
            }
        }
        stage('Approval') {
            steps {
                input "Do you want to proceed with deployment?"
            }
        }
        stage('Deploy') {
            steps{
                echo 'Deploying application...'
            }
        }
    }
    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs!'
            sh 'exit 1'
        }
        always {
            echo 'Pipeline completed (success or failure).'
        }
    }
}
