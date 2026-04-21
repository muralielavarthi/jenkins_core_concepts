pipeline{
    agent {label 'nodejs-20'}

    environment {
        NODE_ENV = 'production'
        PROJECT = 'calc'
    }
    options {
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    parameters {
        string(name: 'APP_VERSION', defaultValue: '1.0.0', description: 'Version of the application to build')
    }
    stages{
        stage('Build') {
            steps {
                echo "Building application version: ${params.APP_VERSION}"
                echo "Using NODE_ENV: ${env.NODE_ENV}"
                echo "Project: ${env.PROJECT}"
            }
        }
        stage('Test') {
            steps {
                echo "Running tests for version: ${params.APP_VERSION}"
                echo "Project: ${env.PROJECT}"
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying ${env.PROJECT} v${params.APP_VERSION}"
            }
        }
    }
}

