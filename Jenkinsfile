pipeline {
    agent any

    tools {
        maven 'ApacheMaven'
    }

    options {
        skipDefaultCheckout true
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
    }

    post {
        always {
            slackSend channel: '#team', color: 'green', message: "The pipeline ${currentBuild.fullDisplayName} result."
        }
    }
}