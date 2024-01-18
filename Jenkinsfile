pipeline {
    agent any

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
                script {
                    withCredentials([usernamePassword(credentialsId: '99', usernameVariable: 'DEPLOY_USER', passwordVariable: 'DEPLOY_USER_PSW')]) {
                        sh "sshpass -p ${env.DEPLOY_USER_PSW} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.37:/var/www/html/"
                    }
                }
            }
        }

        stage('Confirmation Dev') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to test') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: '99', usernameVariable: 'DEPLOY_USER', passwordVariable: 'DEPLOY_USER_PSW')]) {
                        sh "sshpass -p ${env.DEPLOY_USER_PSW} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.39:/var/www/html/"
                    }
                }
            }
        }

        stage('Confirmation test server') {
            steps {
                input(id: 'confirmDeployment', message: 'Review the test environment. If everything looks good, approve for Development.', ok: 'Deploy')
            }
        }

        stage('Deploy to main Server') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: '99', usernameVariable: 'DEPLOY_USER', passwordVariable: 'DEPLOY_USER_PSW')]) {
                        sh "sshpass -p ${env.DEPLOY_USER_PSW} scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/SOHOpipeline_test/index.html ${env.DEPLOY_USER}@192.168.0.41:/var/www/html/"
                    }
                }
            }
        }
    }
}
