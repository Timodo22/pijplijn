pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Stap 1: Ophalen van de broncode uit de Git-repository (in dit geval is er geen broncode)
                // Leeg laten omdat we geen broncode ophalen
            }
        }
        stage('Copy HTML to Server') {
            steps {
                // Stap 2: Kopieer het index.html-bestand naar de Linux-server via SSH
                script {
                    def remoteServer = 'user@your-server-ip' // Vervang met je eigen gebruikersnaam en server-IP
                    def remoteDirectory = '/path/to/remote/directory' // Vervang met het pad naar de doelmap op de server

                    sh "scp index.html ${remoteServer}:${remoteDirectory}"
                }
            }
        }
    }
}
