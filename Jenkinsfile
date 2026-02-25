pipeline {
    agent any

    environment {
        SAUCE_USERNAME = credentials('sauce-username')
        SAUCE_ACCESS_KEY = credentials('sauce-access-key')
    }

    stages {
        stage('Run Sauce Labs Test') {
            steps {
                withEnv([
                    "EMULATOR=${params.SIMULATOR}",
                    "ANDROID_VERSION=${params.ANDROID_VERSION}",
                ]) {
                    sh 'npm install saucectl'
                    sh 'npx saucectl run'
                }
            }
        }
    }

    // post {
    //     always {
    //         cleanWs()
    //     }
    // }
}