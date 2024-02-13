
#!groovy
// it means the libraries will be downloaded and accessible at run time
@Library('roboshop-shared-library') _

def configMap = [
    application: "nodeJSVM",
    component: "catalogue"
]
env

// this is .groovy file name and function inside it.
// if not master then trigger pipeline
if ( ! env.BRANCH_NAME.equalsIgnoreCase('master')) {
pipelineDecision.decidePipeline(configMap)
=======
pipeline {
    agent {node { label 'Agent-1'}}
    environment
    //here if you create any variable you will have global access, since it is environment no need of def
    packageVersion = stop on 37:06

    stages {
        stage ('Get version'){
            steps {
                script{
                    def packageJson = readJSON file: 'package.json'
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
            }
        }

        //instrall pipeline utility steps plugin, if not installed
        stage('Publish Artifact') {
            steps {
                nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',

   
                    nexusUrl: '44.215.110.249:8081'
                    groupId: 'com.roboshop',
                    version: '1.0.0',
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
    }
    post {
        always {
            echo 'cleaning up workspace'
            deleteDir()
       
}
else{
    echo "master PROD deployment should happen through CR"
}