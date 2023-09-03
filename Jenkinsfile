pipeline {
    agent any

    stages {
        stage('Checkout') {
    steps {
        checkout([$class: 'GitSCM', 
            branches: [[name: '*/master']], 
            userRemoteConfigs: [[url: 'https://github.com/rjakkula-rahul/rahul-github.git', credentialsId: 'rahul']]])
    }
}


        stage('Build and Test') {
            steps {
                // Build the project and run tests using Maven
                sh 'mvn clean test'
            }
        }

        stage('Generate Allure Report') {
            steps {
                // Generate Allure report
                sh 'allure generate target/allure-results -o target/allure-report'
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
