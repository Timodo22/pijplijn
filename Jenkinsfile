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

                    // Kopieer het index.html-bestand naar de webserver met scp en schakel hostverificatie uit
                    sh " index.html ${serverUsername}@${serverIP}:${remotePath}"
                }
            }
        }
    }
}
