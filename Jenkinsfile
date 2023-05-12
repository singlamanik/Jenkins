pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Fetch the source code from the directory path specified by the environment variable."
                echo "Compile the code and generate any necessary artifacts."
            }
        }

        stage('Test') {
            steps {
                echo "Run unit tests."
                echo "Run integration tests."
            }
        }

        stage('Code Quality Check') {
            steps {
                echo "Check the quality of the code."
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploy the application to a testing environment specified by the environment variable."
            }
        }

        stage('Approval') {
            steps {
                echo "Waiting for approval..."
                sleep time: 10, unit: 'SECONDS'
            }
        }

        stage('Deploy to Production') {
            when {
                environment name: 'APPROVED', value: 'true'
            }
            steps {
                echo "Deploy the code to the production environment ${PRODUCTION_ENVIRONMENT}."
            }
        }
    }
}
