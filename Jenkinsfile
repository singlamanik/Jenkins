pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                // Use Maven as the build automation tool
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                // Use JUnit for unit tests
                sh 'mvn test'
                
                // Use a test automation tool like Selenium for integration tests
                sh 'mvn integration-test'
            }
        }

        stage('Code Analysis') {
            steps {
                // Use a code analysis tool like SonarQube
                // Ensure SonarQube is properly configured in Jenkins
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                // Use a security scanning tool like OWASP ZAP
                // Ensure OWASP ZAP is properly installed and configured in Jenkins
                sh 'zap-baseline.sh -t <target-url>'
            }
        }

        stage('Deploy to Staging') {
            steps {
                // Use a deployment tool or script to deploy the application to a staging server
                sh 'ansible-playbook -i inventory/staging deploy.yml'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                // Use test automation tools to run integration tests on the staging environment
                sh 'mvn integration-test'
            }
        }

        stage('Deploy to Production') {
            steps {
                // Use a deployment tool or script to deploy the application to a production server
                sh 'ansible-playbook -i inventory/production deploy.yml'
            }
        }
    }

    post {
        always {
            // Send notification emails with status and logs
            emailext body: '${SCRIPT, template="groovy-html.template"}',
                subject: "Pipeline Status: ${currentBuild.result}",
                to: "email@example.com",
                mimeType: 'text/html'
        }
    }
}
