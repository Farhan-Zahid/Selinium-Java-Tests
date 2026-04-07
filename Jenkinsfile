pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Farhan-Zahid/Selinium-Java-Tests'
            }
        }

        stage('Run Tests') {
            steps {
                bat '"C:\\Program Files\\Apache\\Maven\\apache-maven-3.9.14\\bin\\mvn.cmd" clean test'
            }
        }
    }

    post {
        always {
            junit testResults: '**/target/surefire-reports/*.xml', allowEmptyResults: true
        }
    }
}