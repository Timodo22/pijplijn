pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Haal de broncode op van je repository (bijvoorbeeld GitHub)
                checkout scm
            }
        }

        stage('Kopieer naar webserver') {
            steps {
                script {
                    // Vervang 'jouw-gebruikersnaam' door de gebruikersnaam van de webserver
                    // Vervang 'jouw-server-ip' door het IP-adres van de webserver
                    // Vervang '/var/www/html/' door het pad waar je index.html-bestand moet worden gekopieerd

                    def serverUsername = 'student'
                    def serverIP = '192.168.1.18'
                    def remotePath = '/var/www/html/'

                    // Het pad naar de SSH-privésleutel op de Jenkins-server
                    def sshKeyPath ='secret.key'          //'~/.ssh/id_rsa'

                    // Kopieer het index.html-bestand naar de webserver met scp en gebruik SSH-sleutel voor authenticatie
                    sh "scp -i ${sshKeyPath} index.html ${serverUsername}@${serverIP}:${remotePath}"
                }
            }
        }
    }
}
