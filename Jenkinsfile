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
    }
}
