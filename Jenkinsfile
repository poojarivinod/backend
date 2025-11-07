// In google search as jenkins pipeline syntax --> pipeline syntax(jenkins) --> click on pipeline --> copy the code below this Declarative Pipeline fundamentals 
pipeline {
    agent { label 'AGENT-1' }
    environment { 
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
        ACC_ID = '695862934667'
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
        stage('Insatll Dependencies') {
            steps {
                script{
                    sh """
                        npm install
                    """
                }
            }
        }
        stage('Docker Build') {
            steps {
                script{
                    // search in google as "aws credentials in jenkins" --> AWS Credentials {for download "AWS Credentials Plugin" in Jenkins}
                    // search in google as "aws credentials in jenkins" --> GeeksforGeeks(How to use AWS Credentials in Jenkins Pipeline)
                    // within this block, code will bind with credentials, after coming out of this block, credentials deletes automatically
                    // when this stage is executing, jenkins will read the aws-creds, it will setup the aws configure for the code in this block.
                    withAWS(region: 'us-east-1', credentials: 'aws-creds') {
                    sh """
                        aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com
                        docker build -t ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion} .
                        docker push ${ACC_ID}.dkr.ecr.us-east-1.amazonaws.com/${project}/${component}:${appVersion}
                    """
                    }
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