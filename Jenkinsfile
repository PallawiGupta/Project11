pipeline {
    agent any

    parameters {
        string(name: 'GIT_REPO', description: 'Git Repository URL', defaultValue: 'https://github.com/PallawiGupta/Project11.git')
        string(name: 'GIT_BRANCH', description: 'Git Branch', defaultValue: 'master')
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    def gitCheckout = checkout([$class: 'GitSCM', 
                        branches: [[name: params.GIT_BRANCH]], 
                        doGenerateSubmoduleConfigurations: false, 
                        extensions: [], 
                        submoduleCfg: [], 
                        userRemoteConfigs: [[url: params.GIT_REPO]]
                    ])
                    if (gitCheckout) {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'FAILURE'
                        error("Git checkout failed")
                    }
                }
            }
        }

        stage('Deploy to Apache') {
            steps {
                script {
                    def sourceDir = "C:\\Users\\palla\\Desktop\\html\\1st Sem\\ass11"
                    def targetDir = ""C:\\Users\\palla\\Desktop\\httpd-2.4.58-win64-VS17\\Apache24""
                    def copyResult = bat(script: "xcopy /s /e /y \"$sourceDir\" \"$targetDir\"", returnStatus: true)
                    if (copyResult == 0) {
                        currentBuild.result = 'SUCCESS'
                    } else {
                        currentBuild.result = 'FAILURE'
                        error("Code deployment to Apache failed")
                    }
                }
            }
        }
    }

    post {
        failure {
            emailext subject: "Jenkins Build Failed: \${currentBuild.fullDisplayName}",
                     body: "The Jenkins build for \${currentBuild.fullDisplayName} has failed. Please investigate.",
                     recipientProviders: [culprits()]
        }
        success {
            emailext subject: "Jenkins Build Succeeded: \${currentBuild.fullDisplayName}",
                     body: "The Jenkins build for \${currentBuild.fullDisplayName} has succeeded.",
                     recipientProviders: [culprits()]
        }
    }
}
