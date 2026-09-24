pipeline {
    agent any

    parameters {
        booleanParam(name: 'SEND_EMAIL', defaultValue: false, description: 'Check this box to send a notification email upon completion.')
    }

    environment {
        APP_NAME    = 'InventoryManager'
        APP_VERSION = '1.4.2'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from repository...'
            }
        }

        stage('Build') {
            steps {
                echo "Compiling app_name.py for ${env.APP_NAME} version ${env.APP_VERSION}..."
                bat 'python -m py_compile app_name.py'
            }
        }

        stage('Send Notification') {
            when {
                environment name: 'SEND_EMAIL', value: 'true'
            }
            steps {
                echo "Sending notification for ${env.APP_NAME} v${env.APP_VERSION}..."
                echo "Mail Subject: ${env.APP_NAME} v${env.APP_VERSION} Build Status"
            }
        }
    }
}
