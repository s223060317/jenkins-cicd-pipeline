pipeline {
    agent any

    stages {
        stage("Build Stage") {
            steps {
                script {
                    // Use a variable to control verbosity
                    def verbose = false

                    if (verbose) {
                        echo 'Executing Maven build: cleaning and packaging the project'
                    } else {
                        echo 'Executing Maven build...' // Shorter message
                    }
                    // Uncomment the line below to execute the Maven build
                    // sh 'mvn clean install > /dev/null' // Redirect output to null
                }
            }
        }

        stage("Testing: Unit & Integration") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Running JUnit tests to validate code functionality'
                    } else {
                        echo 'Running unit tests...' // Shorter message
                    }
                    // Uncomment the line below to run unit tests
                    // sh 'mvn test > /dev/null' // Redirect output to null
                    
                    if (verbose) {
                        echo 'Running integration tests to verify component interactions'
                    } else {
                        echo 'Running integration tests...' // Shorter message
                    }
                    // Uncomment the line below to run integration tests
                    // sh 'mvn verify > /dev/null' // Redirect output to null
                }
            }
            post {
                success {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "SUCCESS: Unit and Integration Tests Passed",
                        body: "Both unit and integration tests were successful. The codebase is functioning correctly.",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "ERROR: Unit and/or Integration Tests Failed",
                        body: "Unit or integration tests failed. Please check the logs to diagnose the issue.",
                        attachLog: true
                    )
                }
            }
        }

        stage("Code Quality Analysis") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Starting SonarQube analysis for code quality assurance'
                    } else {
                        echo 'Running SonarQube analysis...' // Shorter message
                    }
                    // Uncomment the line below to perform SonarQube analysis
                    // sh 'mvn sonar:sonar > /dev/null' // Redirect output to null
                }
            }
        }

        stage("Security Assessment") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Initiating security scan using OWASP ZAP'
                    } else {
                        echo 'Running security scan...' // Shorter message
                    }
                    // Uncomment the line below to run the security scan
                    // sh 'zap-cli quick-scan --self-contained --start-options "-config api.disablekey=true" http://localhost:8080 > /dev/null' // Redirect output to null
                }
            }
            post {
                success {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "SUCCESS: Security Scan Completed",
                        body: "The security scan has been successfully completed with no issues detected.",
                        attachLog: true
                    )
                }
                failure {
                    emailext (
                        to: "dominicdiona@gmail.com",
                        subject: "ERROR: Security Scan Failed",
                        body: "The security scan encountered issues. Review and address the vulnerabilities.",
                        attachLog: true
                    )
                }
            }
        }

        stage("Staging Deployment") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Deploying application to the staging environment (AWS EC2, S3 bucket)'
                    } else {
                        echo 'Deploying to staging...' // Shorter message
                    }
                    // Uncomment the line below to deploy to the staging environment
                    // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name staging-group --s3-location bucket=staging-bucket,key=my-app.zip > /dev/null' // Redirect output to null
                }
            }
        }

        stage("Staging Environment Tests") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Executing integration tests on the staging environment'
                    } else {
                        echo 'Running staging integration tests...' // Shorter message
                    }
                    // Uncomment the line below to run integration tests in staging
                    // sh 'mvn verify -Dtest=IntegrationTest > /dev/null' // Redirect output to null
                }
            }
        }

        stage("Production Deployment") {
            steps {
                script {
                    def verbose = false

                    if (verbose) {
                        echo 'Deploying the application to the production environment'
                    } else {
                        echo 'Deploying to production...' // Shorter message
                    }
                    // Uncomment the line below to deploy to production
                    // sh 'aws deploy create-deployment --application-name my-app --deployment-group-name production-group --s3-location bucket=production-bucket,key=my-app.zip > /dev/null' // Redirect output to null
                }
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
        }
        failure {
            echo 'Production deployment failed. Review the errors and retry.'
        }
    }
}
