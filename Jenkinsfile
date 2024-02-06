pipeline {
    agent { node { label 'Agent-1' } }
    //here if you create any variable you will have global access, since it is environment no need of def
    environment {
        packageVersion = '' 
    }
    stages {
        stage('Get version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    packageVersion = packageJson.version 
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
                sh 'zip -r catalogue.zip ./* --exclude=.git --exclude=.zip'
            }
        }
        stage('SAST') {
            steps {
                echo "SAST Done"
                echo "package version: $packageVersion"
            }
        }

        // Install the pipeline utility steps plugin if not installed
        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: '172.31.11.142:8081/', // Add http:// here
                    groupId: 'com.roboshop',
                    version: "$packageVersion",
                    repository: 'catalogue',
                    credentialsId: 'nexus-auth',
                    artifacts: [
                        [artifactId: 'catalogue',
                        classifier: '',
                        file: 'catalogue.zip',
                        type: 'zip']
                    ]
                )
            }
        }
    
        // This job will wait until the downstream job is over
        stage('Deploy') {
            steps {
                script {
                    echo "Deployment"
                    def params = [
                        string(name: 'version', value: "${packageVersion}")
                    ]
                    build job: '../catalogue-deploy', wait: true, parameters: params // Use the job name, not relative path
                }
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
