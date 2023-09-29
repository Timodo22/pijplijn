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

                    def hostKeyFingerprint = 'ssh-ed25519 255 60k2X4blYxkcniIRj82ABN/MvBGaDaQyeecrj8FusXk'

                    if (isUnix()) {
                        sh """
                            echo y | winscp.com /command "option batch abort" "option confirm off" "open scp://${serverUsername}@${serverAddress}" "option sshhostkey ${hostKeyFingerprint}" "put -r -i /path/to/your/private/key ./* ${serverDestination}/" "exit"
                        """
                    } else {
                        bat """
                            echo y | winscp.com /command "option batch abort" "option confirm off" "open scp://${serverUsername}@${serverAddress}" "option sshhostkey ${hostKeyFingerprint}" "put -r -i C:\\path\\to\\your\\private\\key .\\* ${serverDestination}\\" "exit"
                        """
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
