pipeline {
    agent {node { label 'Agent-1'}}
    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Unit test') {
            steps {
                echo 'unit testing is done here'
            }
        }
        // Run SonarScanner with the fetched configuration file
        stage('Sonar Scan') {
            steps {
                sh 'ls -ltr'
                sh 'sonar-scanner'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deployment"
            }
        }
    }
}
