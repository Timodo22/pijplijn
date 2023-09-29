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
                    def serverDestination = '/var/www/html/'

                    // Vervang 'C:/path/to/your/private/key' door het pad naar je SSH-private sleutel
                    def sshPrivateKeyPath = 'C:/path/to/your/private/key'

                    // SCP-commando om bestanden te kopiëren
                    bat """
                        winscp.com /command "option batch abort" "option confirm off" "open scp://${serverUsername}@${serverAddress}" "put -r -i ${sshPrivateKeyPath} ./* ${serverDestination}" "exit"
                    """
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
