pipeline {
    agent any
    
    stages {
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    // Assuming you have already installed and configured SonarQube Scanner
                    sh 'sonar-scanner'
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    waitForQualityGate()
                }
            }
        }
    }
    
    post {
        success {
            echo 'SonarQube analysis successful!'
        }
        failure {
            echo 'SonarQube analysis failed! Check Jenkins logs for details.'
        }
    }
}
