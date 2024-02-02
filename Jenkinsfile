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
        // // Run SonarScanner with the fetched configuration file
        // stage('Sonar Scan') {
        //     steps {
        //         sh 'ls -ltr'
        //         sh 'sonar-scanner'
        //     }
        // }
        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r ./* --execlude=.git'
            }
        }
    }
    post {
        always {
            echo 'cleaning up workspace'
            // deleteDir()
        }
    }
}
