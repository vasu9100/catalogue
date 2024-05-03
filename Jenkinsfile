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

    parameters {
        choice(name: 'action', choices: ['clone', 'build']) // Added comma after 'action'
    }

    environment {
        Packageversion = '' 
    }

    stages {
        stage('clone') {
            when {
                expression {
                    params.action == 'clone'
                }
            }
            steps { // Changed 'script' to 'steps'
                script {
                    def packagejson = readJSON file: 'package.json'
                    Packageversion = packagejson.version

                    echo "app version: ${env.Packageversion}" // Corrected variable reference syntax
                }
            }
        }
    }
}
