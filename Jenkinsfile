pipeline {
    agent { label 'nodejs-20' }

    environment {
        DEPLOY_ENV = 'production'
    }

    stages {

        // Parallel stages with NO dependency - run simultaneously
        stage('Parallel Independent') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        echo 'Running unit tests'
                    }
                }
                stage('Code Lint') {
                    steps {
                        echo 'Running linter'
                    }
                }
                stage('Security Scan') {
                    steps {
                        echo 'Running security scan'
                    }
                }
            }
        }

        // Sequential stage that depends on the parallel stages above passing
        stage('Build') {
            steps {
                echo 'Building application - depends on tests, lint and scan passing'
            }
        }

        // Parallel stages with shared dependency - both need Build to finish first
        stage('Parallel Post-Build') {
            parallel {
                stage('Build Docker Image') {
                    steps {
                        echo 'Building Docker image - depends on Build stage'
                    }
                }
                stage('Generate Reports') {
                    steps {
                        echo 'Generating test reports - depends on Build stage'
                    }
                }
            }
        }

        // Final stage with dependency on all above
        stage('Deploy') {
            when {
                expression { env.DEPLOY_ENV == 'production' }
            }
            input {
                message 'Ready to deploy?'
                ok 'Yes, deploy now'
            }
            steps {
                echo "Deploying ${env.DEPLOY_ENV} environment"
            }
        }
    }
}


