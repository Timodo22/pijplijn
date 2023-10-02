pipeline {
    agent any

    stages {
        stage('Checkout from GitHub') {
            steps {
                // Check out your code from GitHub.
                script {
                    def scmVars = checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'test']], // You can change the branch as needed
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [$class: 'CloneOption', noTags: false, reference: '', shallow: false],
                            [$class: 'CleanBeforeCheckout'],
                        ],
                        userRemoteConfigs: [[url: 'https://github.com/Timodo22/pijplijn.git']] // Replace with your GitHub repo URL
                    ])
                }
            }
        }

        stage('Overwrite HTML files on Server') {
            steps {
                // Copy HTML files from the checked-out repository to the server, overwriting existing files.
                sh 'sshpass -p student scp -o StrictHostKeyChecking=no  /var/lib/jenkins/workspace/Multipipeline_test/index.html student@192.168.1.18:/var/www/html/'
            }
        }
    }
}
