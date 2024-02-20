pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/TeamNetrunners/ramitest'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }
        
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'
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
            echo 'Build and SonarQube analysis successful!'
        }
        failure {
            echo 'Pipeline failed! Check Jenkins logs for details.'
        }
    }
}
