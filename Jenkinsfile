pipeline {
    agent any

    environment {
        DEPLOY_USER = credentials('99')
    }

    stages {
        stage('Checkout from GitHub (Test)') {
            steps {
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

        stage('Deploy to Dev Server') {
            steps {
                sh "sshpass -p ${env.DEPLOY_USER} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.37:/var/www/html/"
            }
        }

        stage('Confirmation Dev') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to test') {
            steps {
                sh "sshpass -p ${env.DEPLOY_USER} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.39:/var/www/html/"
            }
        }

        stage('Confirmation test server') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to main Server') {
            steps {
                sh "sshpass -p ${env.DEPLOY_USER} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.41:/var/www/html/"
            }
        }
    }
}
