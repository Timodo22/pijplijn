pipeline {
    agent any

    stages {
        stage('Checkout from GitHub (Test)') {
            steps {
                // Check out your code from the "test" branch on GitHub.
                script {
                    def scmVars = checkout([
                        $class: 'GitSCM',
                        branches: [[name: 'test']],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [$class: 'CloneOption', noTags: false, reference: '', shallow: false],
                            [$class: 'CleanBeforeCheckout'],
                        ],
                        userRemoteConfigs: [[url: 'https://github.com/Timodo22/pijplijn.git']]
                    ])
                }
            }
        }

        stage('Deploy to Test Server') {
            steps {
                // Copy HTML files from the "test" branch to the test server.
                sh 'sshpass -p student scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Multipipeline_test/index.html student@192.168.1.18:/var/www/html/'
            }
        }

        stage('Confirmation') {
            steps {
                // Prompt for confirmation before proceeding.
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for deployment.', ok: 'Deploy')
            }
        }

        stage('Push to Main Branch') {
            steps {
                // Switch to the "main" branch and copy the index.html from the "test" branch.
                sh 'git checkout main'
                sh 'git checkout test -- /var/lib/jenkins/workspace/Multipipeline_test/index.html'
                sh 'git commit -m "Copy index.html from test to main"'
                sh 'git push origin main'
            }
        }

        stage('Deploy to Main Server') {
            steps {
                // Copy HTML files from the "main" branch to the main server.
                sh 'sshpass -p student scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/Multipipeline_test/index.html student@192.168.1.18:/var/www/html/'
            }
        }
    }
}
