pipeline {
    agent {node { label 'Agent-1'}}
    //here if you create any variable you will have global access, since it is environment
    environment{
        packageVersion = ''
    }
    stages {
        stage ('Get version'){
            steps {
                script{
                    def packageJson = readJSON(file: 'package.json')
                    def packageVersion = packageJson.version
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
        // Run SonarScanner with the fetched configuration file
        stage('Sonar Scan') {
            steps {
                echo 'sonar scan done'
            }
        }

        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
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
