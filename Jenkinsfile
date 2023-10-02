pipeline {
    agent any // Dit betekent dat de pipeline op elke beschikbare agent kan draaien

    environment {
        // Voeg hier eventuele omgevingsvariabelen toe
        SSH_HOST = '192.168.1.18'
        SSH_USER = 'student'
        GIT_REPO = 'https://github.com/Timodo22/pijplijn.git'
        GIT_BRANCH = 'test' // of de naam van de tak die je wilt gebruiken
    }

stage('Haal code op van GitHub') {
    steps {
        // Haal de code op van GitHub-repository zonder credentials
        git branch: env.GIT_BRANCH, url: env.GIT_REPO
    }
    post {
        always {
            echo 'Stappen in de post-sectie'
        }
    }
}

        stage('Kopieer naar webserver') {
            steps {
                // Kopieer het index.html-bestand naar de externe webserver via SSH
                script {
                    sh """
                        sshpass -p ${SSH_PASSWORD} rsync -avz ./Jenkinsfile ./index.html ./test.txt ./test2.txt ${SSH_USER}@${SSH_HOST}:/var/www/html/
                    """
                }
            }
        }
    }

    post {
        always {
            // Voer optionele stappen uit na de hoofdstappen, indien nodig
        }
    }
}
