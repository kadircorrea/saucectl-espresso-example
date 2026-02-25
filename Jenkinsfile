pipeline {
    agent any
    stages {
        stage('Run Sauce Labs Test') {
            steps {
                withEnv([
                    "EMULATOR=${params.SIMULATOR}",
                    "ANDROID_VERSION=${params.ANDROID_VERSION}",
                    "RETRIES=${params.RETRIES}",
                    "PASS_THRESHOLD=${params.PASS_THRESHOLD}"
                ]) {
                    sh 'npm install saucectl'
                    sh 'npx saucectl run'
                }
            }
        }
    }
    post {
        always {
            cleanWs()
        }
    }
}