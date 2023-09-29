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
                    def password = 'student'

                    if (isUnix()) {
                        sh """
                            rsync -avz --progress ./* ${serverUsername}@${serverAddress}:${serverDestination}/
                        """
                    } else {
                        // Op Windows kun je PuTTY-plink en pscp gebruiken
                        bat """
                            plink -ssh -l ${serverUsername} -pw ${password} -P 22 ${serverAddress} "pscp -r -pw ${password} C:\\path\\to\\your\\source\\* ${serverUsername}@${serverAddress}:${serverDestination}/"
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
