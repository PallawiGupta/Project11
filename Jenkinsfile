pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Check out the code from your GitHub repository
                checkout([$class: 'GitSCM', 
                    branches: [[name: 'main']], 
                    doGenerateSubmoduleConfigurations: false, 
                    extensions: [], 
                    submoduleCfg: [], 
                    userRemoteConfigs: [[url: 'https://github.com/PallawiGupta/Project11']]
                ])
            }
        }

        stage('Deploy to Apache') {
            steps {
                // Copy the code to the Apache document root directory
                bat script: '''
                    xcopy /s /e /y "C:\\Users\\palla\\Desktop\\html\\1st Sem\\ass11" "C:\\Apache24\\htdocs"

                '''
            }
        }
    }
}
