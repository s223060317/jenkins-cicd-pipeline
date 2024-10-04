pipeline {
    agent any

    stages {
        stage("Build Stage") {
            steps {
                echo 'Executing Maven build: cleaning and packaging the project'
                // Uncomment the line below to execute the Maven build
                // sh 'mvn clean install'
            }
        }

        stage("Testing: Unit & Integration") {
            steps {
                echo 'Running JUnit tests to validate code functionality'
                // Uncomment the line below to run unit tests
                // sh 'mvn test'
                
                echo 'Running integration tests to verify component interactions'
                // Uncomment the line below to run integration tests
                // sh 'mvn verify'
            }
            post {
                success {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "SUCCESS: Unit and Integration Tests Passed",
                        body: "${currentBuild.fullDisplayName} - Unit and integration tests passed.\nBuild log:\n${currentBuild.log}",
                        attachLog: false  // Logs included in body instead of attachment
                    )
                }
                failure {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "ERROR: Unit and/or Integration Tests Failed",
                        body: "${currentBuild.fullDisplayName} - Unit or integration tests failed. Please review the logs.\nBuild log:\n${currentBuild.log}",
                        attachLog: false  // Logs included in body instead of attachment
                    )
                }
            }
        }

        stage("Code Quality Analysis") {
            steps {
                echo 'Starting SonarQube analysis for code quality assurance'
                // Uncomment the line below to perform SonarQube analysis
                // sh 'mvn sonar:sonar'
            }
            post {
                success {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "SUCCESS: SonarQube Analysis Completed",
                        body: "SonarQube analysis has successfully completed.",
                        attachLog: false
                    )
                }
                failure {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "ERROR: SonarQube Analysis Failed",
                        body: "SonarQube analysis encountered errors. Review the logs for details.",
                        attachLog: false
                    )
                }
            }
        }

        stage("Security Assessment") {
            steps {
                echo 'Initiating security scan using OWASP ZAP'
                // Uncomment the line below to run the security scan
                // sh 'zap-cli quick-scan --self-contained --start-options "-config api.disablekey=true" http://localhost:8080'
            }
            post {
                success {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "SUCCESS: Security Scan Completed",
                        body: "The security scan has been successfully completed with no issues detected.",
                        attachLog: false  // Attach log if needed
                    )
                }
                failure {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "ERROR: Security Scan Failed",
                        body: "The security scan encountered issues. Review and address the vulnerabilities.",
                        attachLog: false  // Attach log if needed
                    )
                }
            }
        }

        stage("Staging Deployment") {
            steps {
                echo 'Deploying application to the staging environment (AWS EC2, S3 bucket)'
                // Uncomment the line below to deploy to the staging environment
                // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name staging-group --s3-location bucket=staging-bucket,key=my-app.zip'
            }
        }

        stage("Staging Environment Tests") {
            steps {
                echo 'Executing integration tests on the staging environment'
                // Uncomment the line below to run integration tests in staging
                // sh 'mvn verify -Dtest=IntegrationTest'
            }
        }

        stage("Production Deployment") {
            steps {
                echo 'Deploying the application to the production environment'
                // Uncomment the line below to deploy to production
                // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name production-group --s3-location bucket=production-bucket,key=my-app.zip'
            }
        }

        stage("Finalization") {
            steps {
                echo 'Pipeline execution complete'
            }
        }
    }

    post {
        success {
            echo 'Production deployment successful!'
            emailext (
                to: "dominicdiona@gmail.com",
                subject: "SUCCESS: Pipeline Execution Completed",
                body: "The pipeline has completed successfully. All stages were executed without errors.",
                attachLog: false  // Attach log if necessary
            )
        }
        failure {
            echo 'Production deployment failed. Review the errors and retry.'
            emailext (
                to: "dominicdiona@gmail.com",
                subject: "ERROR: Pipeline Execution Failed",
                body: "The pipeline encountered errors. Review the logs and retry.",
                attachLog: false  // Attach log if necessary
            )
        }
    }
}
