pipeline {
    agent any

    tools {
        maven 'Maven-3.9'
        jdk 'JDK-17'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Farhan-Zahid/Selinium-Java-Tests'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test -Dsurefire.suiteXmlFiles=testng.xml'
            }
        }

        stage('Publish Reports') {
            steps {
                allure includeProperties: false,
                       jdk: '',
                       results: [[path: 'target/allure-results']]
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/screenshots/**', allowEmptyArchive: true
        }
        failure {
            emailext to: 'team@company.com',
                     subject: "Test Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                     body: "Check build: ${env.BUILD_URL}"
        }
    }
}