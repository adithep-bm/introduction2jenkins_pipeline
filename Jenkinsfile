pipeline {
    agent any
    parameters {
        booleanParam(name: 'RUN_DEPLOY', defaultValue: false, 
        description: 'Should we deploy?')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }
        state('Test in Parallel') {
            parallel{
                stage('Unit Tests') {
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
        stage('Test') {
            steps {
                sh 'echo "All tests passed!" > result.txt'
                archiveArtifacts artifacts: 'result.txt', fingerprint: true
            }
        }
        stage('Deploy') {
            when {
                expression { return params.RUN_DEPLOY }
            }
            steps{
                echo 'Deploying application...'
            }
        }
    }
}
