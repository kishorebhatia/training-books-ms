def serviceName = "training-books-ms"
def registry = "localhost:5000"
def flow

node("cd") {
    git "https://github.com/cloudbees/${serviceName}.git"
    flow = load "/mnt/scripts/pipeline-common.groovy"
    flow.runPreDeploymentTests(serviceName, registry)
    flow.build(serviceName, registry)
}
checkpoint "deploy"
node("cd") {
    flow.deploy(serviceName, registry)
    flow.runPostDeploymentTests(serviceName, registry, "http://[IP]:8081")
}
