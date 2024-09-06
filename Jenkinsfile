pipeline {
    agent any

    environment {
        // Add environment variables here if needed
    }

    stages {
        stage('Build') {
            steps {
                script {
                    echo 'Building the code...'
                    // Tool: Maven
                    sh 'mvn clean package'
                }
            }
        }
        
        stage('Unit and Integration Tests') {
            steps {
                script {
                    echo 'Running unit and integration tests...'
                    // Tool: JUnit
                    sh 'mvn test'
                }
            }
        }

        stage('Code Analysis') {
            steps {
                script {
                    echo 'Analyzing code...'
                    // Tool: SonarQube
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                script {
                    echo 'Scanning for security vulnerabilities...'
                    // Tool: OWASP Dependency-Check
                    sh 'dependency-check --project my-project --scan .'
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    echo 'Deploying to staging environment...'
                    // Tool: AWS CLI
                    sh 'aws s3 cp target/my-app.zip s3://my-staging-bucket/my-app.zip'
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                script {
                    echo 'Running integration tests on staging...'
                    // Tool: Custom Integration Tests
                    sh './run_integration_tests.sh'
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    echo 'Deploying to production environment...'
                    // Tool: AWS CLI
                    sh 'aws s3 cp target/my-app.zip s3://my-production-bucket/my-app.zip'
                }
            }
        }
    }

    post {
        success {
            script {
                echo 'Pipeline succeeded.'
                // Email notification for success
                emailext(
                    to: 'dominicdiona@gmail.com',
                    subject: 'Pipeline Success',
                    body: 'The pipeline has succeeded.\n\nBuild logs are attached.',
                    attachLog: true
                )
            }
        }

        failure {
            script {
                echo 'Pipeline failed.'
                // Email notification for failure
                emailext(
                    to: 'dominicdiona@gmail.com',
                    subject: 'Pipeline Failure',
                    body: 'The pipeline has failed.\n\nPlease check the logs for more details.',
                    attachLog: true
                )
            }
        }
    }
}
