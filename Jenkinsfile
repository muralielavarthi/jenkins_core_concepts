pipeline {
    agent { label 'nodejs-20' }

    parameters {
        choice(name: 'DEPLOY_ENV', choices: ['dev', 'staging', 'production'], description: 'Select target environment')
    }

    stages {
        stage('Deploy') {
            when {
                expression { params.DEPLOY_ENV == 'production' }
            }
            input {
                message 'Ready to deploy?'
                ok 'Yes, deploy now'
            }
            steps {
                echo "Deploying ${params.DEPLOY_ENV} environment"
            }
        }
    }
}


