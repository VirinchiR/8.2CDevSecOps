pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                // build steps
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                // test steps
            }
        }
    }

post {
    always {
        emailext(
            subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
            body: """<p>Build Status: ${currentBuild.currentResult}</p>
                     <p>Project: ${env.JOB_NAME}</p>
                     <p>Build Number: ${env.BUILD_NUMBER}</p>
                     <p>URL: <a href='${env.BUILD_URL}'>${env.BUILD_URL}</a></p>""",
            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
            to: 'virinchirawal@gmail.com',
            mimeType: 'text/html'
        )
    }
}        
    failure {
        emailext (
            subject: "FAILURE: ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
            body: "Something went wrong!\nCheck: ${env.BUILD_URL}",
            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
            to: 'your-email@gmail.com'
        )
    }
}

