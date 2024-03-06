// Jenkinsfile
@Library('roboshop-shared-library') _

def configMap = [
    application: "nodeJSEKS",
    component: "catalogue"
]

// Assuming pipelineDecision.decidePipeline(configMap) will trigger the appropriate pipeline based on the configMap
if (!env.BRANCH_NAME.equalsIgnoreCase('master')) {
    pipelineDecision.decidePipeline(configMap)
} else {
    echo "Master PROD deployment should happen through CR"
}
