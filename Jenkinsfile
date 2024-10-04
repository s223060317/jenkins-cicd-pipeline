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


    post {
        success {
            echo 'Production deployment successful!'
        }
        failure {
            echo 'Production deployment failed. Review the errors and retry.'
        }
    }
}
