pipeline {
    agent any

    environment {
        AWS_SAM_STACK_NAME = "sam-app"
    }

    stages {

        stage('Setup') {
            steps {
                sh "pip3 install -r sam-app/tests/requirements.txt"
            }
        }


        stage('Test') {
            steps {
                sh "pytest"
            }
        }

        stage('Build') {
            steps {
                sh "sam build -t sam-app/template.yaml"
            }
        }

        stage('Deploy') {

            environment {
                AWS_ACCESS_KEY_ID = credentials('aws-access-key')
                AWS_SECRET_ACCESS_KEY = credentials('aws-secret-key')
            }

            steps {
                sh "sam deploy -t sam-app/template.yaml --no-confirm-changeset --no-fail-on-empty=changeset"
            }
        }
    }
}