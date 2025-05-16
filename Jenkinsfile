pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/VirinchiR/8.2CDevSecOps.git'
      }
    }

    stage('Install Dependencies') {
      steps {
        sh '/opt/homebrew/bin/npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh '/opt/homebrew/bin/npm test || true'
      }
    }

    stage('Generate Coverage Report') {
      steps {
        sh '/opt/homebrew/bin/npm run coverage || true'
      }
    }

    stage('NPM Audit (Security Scan)') {
      steps {
        sh '/opt/homebrew/bin/npm audit || true'
      }
    }

    // 👇 ADD THIS SONARCLOUD STAGE HERE
    stage('SonarCloud Analysis') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          sh '''
            curl -sSLo sonar-scanner.zip https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.7.0.2747-linux.zip
            unzip sonar-scanner.zip
            ./sonar-scanner-*/bin/sonar-scanner -Dsonar.login=$SONAR_TOKEN
          '''
        }
      }
    }
  }
}
