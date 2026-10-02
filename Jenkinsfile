pipeline {
    agent {
        label "node-24"
    }
    environment {
        SSH_AGENT = "ci-github-ssh-credentials"
    }
    stages {
        stage('prepare') {
            steps {
                container('node') {
                    checkout scm
                    sh """
                        npm ci
                        npm run build
                        # npm run style
                        # npm run lint
                        npm run test
                        npm publish --registry ${env.APW_NPM_REGISTRY}
                    """

//                     sshagent([env.SSH_AGENT]) {
//                         sh """
//                             git push origin $(git rev-parse --abbrev-ref HEAD)
//                             git push --tags
//                         """
//                     }
                }
            }
        }
    }
//     post {
//         unsuccessful {
//             withCredentials([string(credentialsId: 'slack-apwide-notif-url', variable: 'url')]) {
//                 httpRequest([
//                         httpMode       : 'POST',
//                         contentType    : 'APPLICATION_JSON',
//                         requestBody    : """{ "text": "(${GIT_LOCAL_BRANCH}) Documentation links test failed: ${BUILD_URL}", "channel": "development", "username": "Link checker" }""",
//                         responseHandle : 'NONE',
//                         url            : "${url}",
//                         wrapAsMultipart: false
//                 ])
//             }
//         }
//     }
}
