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
                    def serverPassword = 'student'
                    def password = 'student'

                    if (isUnix()) {
                        sh """
                            # Gebruik Git Bash om SSH-opdrachten uit te voeren
                            sshpass -p "${serverPassword}" rsync -avz ./* ${serverUsername}@${serverAddress}:${serverDestination}/
                            rsync -avz --progress --rsh="sshpass -p ${password} ssh -o StrictHostKeyChecking=no -l ${serverUsername}" ./* ${serverUsername}@${serverAddress}:${serverDestination}/
                        """
                    } else {
                        // Op Windows kun je plink (onderdeel van PuTTY) en rsync gebruiken
                        bat """
                            # Gebruik Git Bash om SSH-opdrachten uit te voeren
                            sshpass -p "${serverPassword}" rsync -avz ./* ${serverUsername}@${serverAddress}:${serverDestination}/
                            plink -ssh -l ${serverUsername} -pw ${password} -P 22 ${serverAddress} "rsync -avz --progress /cygdrive/c/path/to/your/source/* ${serverDestination}/"
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
