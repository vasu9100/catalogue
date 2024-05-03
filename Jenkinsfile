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
        Packageversion = '' // Changed 'environments' to 'environment', and removed unnecessary space
    }

    stages {
        stage('clone') {
            steps { // Changed 'script' to 'steps'
                script {
                    env.Packageversion = readJSON(file: 'package.json').version
                    echo "app version: ${env.Packageversion}" // Corrected variable reference syntax
                }
            }
        }
    }
}
