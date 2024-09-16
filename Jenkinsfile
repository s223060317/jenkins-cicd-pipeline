pipeline {
    agent any

    stages {
        stage("Build Stage") {
            steps {
                echo 'Executing Maven build: cleaning and packaging the project'
                // sh 'mvn clean install'
            }
        }

        stage("Testing: Unit & Integration") {
            steps {
                echo 'Running JUnit tests to validate code functionality'
                // sh 'mvn test'
                echo 'Running integration tests to verify component interactions'
                // sh 'mvn verify'
            }
            post {
                success {
                    mail to: "dominicdiona@gmail.com",
                         subject: "SUCCESS: Unit and Integration Tests Passed",
                         body: "Both unit and integration tests were successful. The codebase is functioning correctly."
                }
                failure {
                    mail to: "dominicdiona@gmail.com",
                         subject: "ERROR: Unit and/or Integration Tests Failed",
                         body: "Unit or integration tests failed. Please check the logs to diagnose the issue."
                }
            }
        }

        stage("Code Quality Analysis") {
            steps {
                echo 'Starting SonarQube analysis for code quality assurance'
                // sh 'mvn sonar:sonar'
            }
        }

        stage("Security Assessment") {
            steps {
                echo 'Initiating security scan using OWASP ZAP'
                // sh 'zap-cli quick-scan --self-contained --start-options "-config api.disablekey=true" http://localhost:8080'
            }
            post {
                success {
                    mail to: "dominicdiona@gmail.com",
                         subject: "SUCCESS: Security Scan Completed",
                         body: "The security scan has been successfully completed with no issues detected."
                }
                failure {
                    mail to: "dominicdiona@gmail.com",
                         subject: "ERROR: Security Scan Failed",
                         body: "The security scan encountered issues. Review and address the vulnerabilities."
                }
            }
        }

        stage("Staging Deployment") {
            steps {
                echo 'Deploying application to the staging environment (AWS EC2, S3 bucket)'
                // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name staging-group --s3-location bucket=staging-bucket,key=my-app.zip'
            }
        }

        stage("Staging Environment Tests") {
            steps {
                echo 'Executing integration tests on the staging environment'
                // sh 'mvn verify -Dtest=IntegrationTest'
            }
        }

        stage("Production Deployment") {
            steps {
                echo 'Deploying the application to the production environment'
                // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name production-group --s3-location bucket=production-bucket,key=my-app.zip'
            }
        }

        stage("Complete") {
            steps {
                echo 'Pipeline execution complete'
            }
        }
    }

    post {
        success {
        archiveArtifacts artifacts: 'logs/**', allowEmptyArchive: true
        mail to: "dominicdiona@gmail.com",
             subject: "SUCCESS: Pipeline Completed",
             body: "The pipeline execution was successful.",
             attachmentsPattern: 'logs/**'
    }
    failure {
        archiveArtifacts artifacts: 'logs/**', allowEmptyArchive: true
        mail to: "dominicdiona@gmail.com",
             subject: "ERROR: Pipeline Failed",
             body: "The pipeline failed. Please check the attached log file for details.",
             attachmentsPattern: 'logs/**'
    }
}
