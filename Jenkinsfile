// In google search as jenkins pipeline syntax --> pipeline syntax(jenkins) --> click on pipeline --> copy the code below this Declarative Pipeline fundamentals 
pipeline {
    agent { label 'AGENT-1' }
    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
    }
    options { 
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES') 
        // timeout(time: 5, unit: 'SECONDS')
    } 
    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Mr Jenkins', description: 'Who should I say hello to?')
    //     text(name: 'BIOGRAPHY', defaultValue: '', description: 'Enter some information about the person')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    //     password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
    // }
    stages {
        stage('Read Version') {
            steps {
                script{
                    // search in google as "readjson in jenkins" --> click on Pipeline Utility Steps
                    // jenkins will read the package.json file and store the content into packageJson
                    def packageJson = readJSON file: 'package.json'
                    // we get the version information into the appVersion
                    appVersion = packageJson.version
                    // It will print the appVersion
                    echo "Version is: $appVersion"        
                }
            }
        }
    }  
    stages {
        stage('Insatll Dependencies') {
            steps {
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
    }    
    //In google search as jenkins pipeline syntax --> pipeline syntax(jenkins) --> post
    post { 
        always { 
            echo 'I will always say Hello again!'
            deleteDir() // deletedir option post jenkins --> stack overflow
        }
        failure { 
            echo 'I will run when pipeline is failed'
        }
        success { 
            echo 'I will run when pipeline is success'
        }
    }    
}