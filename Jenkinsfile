pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/NielsTjenkins/Jenkinsfile.git']]])
            }
        }
        stage('Deploy to Test Server') {
            when {
                expression { currentBuild.rawBuild.getBranch().getName() == 'main' }
            }
            steps {
                echo 'Deploying to Test Server'
                pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'main']], userRemoteConfigs: [[url: 'https://github.com/NielsTjenkins/Jenkinsfile.git']]])
            }
        }
        stage('Deploy to Test Server') {
            when {
                expression { currentBuild.rawBuild.getBranch().getName() == 'main' }
            }
            steps {
                echo 'Deploying to Test Server'
                bat '"C:\Program Files\PuTTY\pscp.exe" -i "C:\path\to\private-key.ppk" -r ./* username@10.0.0.26:/var/www/html/'

            }
        }
        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getBranch().getName() == 'main' }
            }
            steps {
                echo 'Deploying to Production Server'


                bat '"C:\Program Files\PuTTY\pscp.exe" -i "C:\path\to\private-key.ppk" -r ./* student@10.0.0.26:/var/www/html/'
            }
        }
    }
}
'
            }
        }
        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getBranch().getName() == 'main' }
            }
            steps {
                echo 'Deploying to Production Server'


                bat 'pscp -i path/to/private-key.ppk -r ./* student@192.168.29.67:/var/www/html/'
            }
        }
    }
}
