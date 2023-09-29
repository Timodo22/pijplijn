pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Deze stap haalt de broncode op uit de Git-repository
                checkout scm
            }
        }

        stage('Copy Files to Web Server') {
            steps {
                // Vervang de placeholders met jouw serverinformatie en bestemmingsmap
                script {
                    def serverUsername = 'student'
                    def serverAddress = '192.168.1.22'
                    def serverDestination = '/var/www/html'

                    if (isUnix()) {
                        sh "rsync -avz -e ssh ./* ${serverUsername}@${serverAddress}:${serverDestination}/"
                    } else {
                        bat "robocopy .\\ \\\\${serverAddress}\\${serverDestination} /E"
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Bestanden zijn succesvol gekopieerd naar de webserver.'
        }
    }
}
