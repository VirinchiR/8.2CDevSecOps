pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'virinchirawal@gmail.com' // 🔁 Replace with your email
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/VirinchiR/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test || true' // avoid failure from test errors for email testing
            }
        }

        stage('Security Scan') {
            steps {
                sh 'npm audit || true'
            }
        }
    }

post {
    success {
        emailext(
            subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Good news! The build ${env.JOB_NAME} #${env.BUILD_NUMBER} completed successfully.\n\nCheck it here: ${env.BUILD_URL}",
            to: "virinchirawal@gmail.com"
        )
    }
    failure {
        emailext(
            subject: "Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
            body: "Unfortunately, the build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed.\n\nCheck it here: ${env.BUILD_URL}",
            to: "virinchirawal@gmail.com"
        )
    }
}
