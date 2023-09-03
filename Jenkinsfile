pipeline {
    agent any

    environment {
        // Define the path to the Allure command-line executable
        ALLURE_HOME = tool name: 'Allure', type: 'io.qameta.allure.jenkins.AllureInstallation'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout your project's source code from your version control system
                checkout scm
            }
        }

        stage('Build and Test') {
            steps {
                // Build your project and run tests
                sh "${tool name: 'Maven'} clean test"
            }
        }

        stage('Generate Allure Report') {
            steps {
                // Generate Allure report
                sh "${ALLURE_HOME}/bin/allure generate target/allure-results -o target/allure-report"
            }
        }
    }

    post {
        always {
            // Archive the Allure report files as an artifact
            archiveArtifacts artifacts: 'target/allure-report/**'
            // Publish the Allure report to Jenkins
            allure([
                includeProperties: false,
                jdk: '',
                properties: [],
                reportBuildPolicy: 'ALWAYS',
                results: [[path: 'target/allure-results']]
            ])
        }
    }
}
