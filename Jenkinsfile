pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Fetching the source code from the directory path specified by the environment variable."
                echo "Compiling the code and generating any necessary artifacts."
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo "Running unit tests."
                echo "Running integration tests."
            }
        }

        stage('Code Analysis') {
            steps {
                echo "Checking the quality of the code using a code analysis tool."
            }
        }

        stage('Security Scan') {
            steps {
                echo "Identifying vulnerabilities using a security scanning tool."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment."
                
            }
        }

        stage('Deploy to Production') {
            
            steps {
                echo "Deploying the code to the production environment."
            }
        }
    }

    post {
        success{
                    emailext attachLog: true,
                    compressLog: true,
                    to: 'singlamanik03@gmail.com',
                    body: 'log is available at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastSuccessfulBuild/log',
                    subject: 'Production Deployment is Successful - Jenkins'
                }
                failure {  
                    emailext attachLog: true,
                    compressLog: true,
                    to: 'singlamanik03@gmail.com',
                    body: 'log is available at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastSuccessfulBuild/log',
                    subject: "Production Deployment is Failed - Jenkins"  
                }
    }
}
