pipeline {
    agent any
    stages {
        stage('###################  Build  #########################') {
            steps {
                // Get code from GitHub repository with credentials
                git credentialsId: '508b241c-2ce7-417d-983d-493a8d4dcef7',
                    url: 'https://github.com/ivanvb07/HelloWorldMaven.git',
                    branch: 'master' 

                // Run Maven on a Unix agent
                sh "mvn clean install"
            }
            post {
                success {
                    script {
                        // Create the tag
                        sh """
                            git config user.email "jenkins@example.com"
                            git config user.name "Jenkins"
                            git tag -a V_2.${BUILD_NUMBER} -m 'Great build' || true
                        """

                        // Push the tag using Git plugin
                        withCredentials([usernamePassword(
                            credentialsId: '508b241c-2ce7-417d-983d-493a8d4dcef7',
                            usernameVariable: 'GIT_USERNAME',
                            passwordVariable: 'GIT_PASSWORD'
                        )]) {
                            sh """
                                git push https://github.com/ivanvb07/HelloWorldMaven.git --tags
                            """
                        }
                    }
                }
            }
        }
    }
}
