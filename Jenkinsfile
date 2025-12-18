pipeline {
    agent any

    stages {
        stage('###################  Build  #########################') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/ivanvb07/HelloWorldMaven.git'
                // Run Maven on a Unix agent.
                sh "mvn clean install"
            }
            post {
                success {
                    script {
                        sh "git tag -a v_2${BUILD_NUMBER} || true"

                        // Pousser le tag avec credentials
                        withCredentials([usernamePassword(
                            credentialsId: '4aa942a6-ae93-413c-afc5-3cfb0029a962',
                            usernameVariable: 'GIT_USERNAME',
                            passwordVariable: 'GIT_PASSWORD'
                        )]) {
                            sh """
                                git config user.email "jenkins@example.com"
                                git config user.name "Jenkins"
                                git push https://github.com/ivanvb07/HelloWorldMaven.git --tags
                            """
                        }
                    }
                }
            }
        }
    }
}
