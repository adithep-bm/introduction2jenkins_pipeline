pipeline {
    agent any
    parameters {
         booleanParam(name: 'BUILD_SUCCESS', defaultValue: false, 
         description: 'Is Build successfully?')
         choice(name: 'ENVIRONMENT', choices: ['dev', 'staging', 'prod'], 
         description: 'Select the deployment environment')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }
        stage('Test in Parallel') {
            parallel {
                stage('Unit Tests') {
                    when {
                        expression { return params.BUILD_SUCCESS }
                    }
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
        stage('Simulate testing') {
            parallel {
                state('Linux') {
                    steps {
                        echo 'Simulating tests on Linux...'
                        sh 'sleep 5'
                    }
                }
                state('Windows') {
                    steps {
                        echo 'Simulating tests on Windows...'
                        sh 'sleep 5'
                    }
                }
            }
        }
        stage('Approval') {
            timeout(time: 1, unit: 'SECONDS')
            steps {
                input "Do you want to proceed with deployment?"
            }
        }
        stage('Deploy') {
            steps{
                echo "Deploying application to environment: ${params.ENVIRONMENT}"
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
