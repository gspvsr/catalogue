pipeline {
    agent {
        node {
            label 'Agent-1'
        }
    }
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
        stage('Fetch SonarQube Configuration') {
            steps {
                // Fetch the SonarQube configuration file from your repository
                sh 'git checkout sonar-project.properties'
            }
        }
        stage('Sonar Scan') {
            steps {
                // Run SonarScanner with the fetched configuration file
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
