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
            junit 'target/surefire-reports/**/*.xml'
            
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
        }
        success {
            mail to: 'onantab47@gmail.com',
                subject: "Completed Pipeline: ${currentBuild.fullDisplayName}",
                body: "Your build completed, please check: ${env.BUILD_URL}"
        }
    }
}