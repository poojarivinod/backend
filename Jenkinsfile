// search in google as "jenkins shared library example phoenix" --> phoenixNAP --> Step 4
// It will search in github with this name('jenkins-shared-library')
// In run time cloned the jenkins-shared-library file
@Library('jenkins-shared-library')_
// It provides the key value pairs to the configMap object
def configMap = [
    project: "expense",
    component: "backend"
]

 echo "$env.BRANCH_NAME"

// if ( ! $env.BRANCH_NAME.equalsIgnoreCase('main') ) {
//     nodeJSEKSpipeline(configMap)
// }
// else{
//     echo "please follow the production process"
// }

// def configMap = [
//     greeting: "Hello, Good Morning"
//]    
// samplePipeline(configMap)
// To run the pipeline within samplePipeline
// samplePipeline.runPipeline