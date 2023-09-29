pipeline {
    agent any

    stages {
        stage('Kopieer bestanden naar server') {
            steps {
                script {
                    // Gegevens van de webserver
                    def serverHost = '192.168.1.22'
                    def serverPort = 22 // Standaard SSH-poort
                    def serverUser = 'student'
                    def serverPassword = 'student'

                    // Bestemming op de server
                    def serverDir = '/var/www/html'

                    // Pad naar de bestanden die je wilt kopiëren
                    def localDir = './lokale_map_met_bestanden/*'

                    // SSH-opdracht om bestanden te kopiëren naar de server
                    sh """
                        sshpass -p ${serverPassword} scp -P ${serverPort} -r ${localDir} ${serverUser}@${serverHost}:${serverDir}
                    """
                }
            }
        }
    }
}
