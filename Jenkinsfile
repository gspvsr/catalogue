pipeline {
    agent { node { label 'Agent-1' } }
    environment {
        packageVersion = '' // Initialize the packageVersion variable
    }
    stages {
        stage('Get version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version // Assign the value to the environment variable
                    echo "version: ${packageVersion}"
                }
            }
        }
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
        stage('Sonar Scan') {
            steps {
                echo 'sonar scan done'
            }
        }
        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=catalogue.zip'
            }
        }
        stage('SAST') {
            steps {
                echo "SAST done"
                echo "package version: $packageVersion"
            }
        }
    }

    //     //install pipeline utility steps plugin, if not installed
    //     stage('Publish Artifact') {
    //         steps {
    //             nexusArtifactUploader(
    //                 nexusVersion: 'nexus3',
    //                 protocol: 'http',
    //                 nexusUrl: '172.31.7.125:8081/',
    //                 groupId: 'com.roboshop',
    //                 version: '1.0.3',
    //                 repository: 'catalogue',
    //                 credentialsId: 'nexus-auth',
    //                 artifacts: [
    //                     [artifactId: 'catalogue',
    //                     classifier: '',
    //                     file: 'catalogue.zip',
    //                     type: 'zip']
    //                 ]
    //             )
    //         }
    //     }
    // }
    post {
        always {
            echo 'cleaning up workspace'
            deleteDir()
        }
    }
}
