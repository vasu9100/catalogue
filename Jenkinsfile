pipeline {
    agent {
        node {
            label 'agent-1'
        }
    }

    options {
        ansiColor('xterm')
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'HOURS') // Corrected syntax for timeout
    }

    

    environment {
        packageversion = '' 
        nexusURL = '44.192.61.27:8081'
    }

    parameters {
        booleanParam(name: 'Deploy', defaultValue: false,)
    }

    stages {
        stage('clone') {
            
            steps { // Changed 'script' to 'steps'
                script {
                    def packagejson = readJSON file: 'package.json'
                    packageversion = packagejson.version

                    echo "app version: $packageversion" // Corrected variable reference syntax
                }
            }
        }

        stage('npm') {
            steps {
                sh """
                    npm install
                """
            }
    
        }

        stage('zipping') {
            steps {
                sh """
                    ls -la
                    zip -q -r catalogue.zip ./* -x ".git" -x "*.zip"
                    ls -ltr

                """
            }
        }

         stage('Publish Artifact') {
            steps {
                 nexusArtifactUploader(
                    nexusVersion: 'nexus3',
                    protocol: 'http',
                    nexusUrl: "${nexusURL}",
                    groupId: 'com.roboshop',
                    version: "${packageversion}",
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

}
