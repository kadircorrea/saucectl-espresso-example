pipeline {
    agent any

    parameters {
        string(name: 'ANDROID_VERSION', defaultValue: '15.0')
        string(name: 'SIMULATOR', defaultValue: 'Generic Medium Phone Emulator')
    }

    environment {
        SAUCE_USERNAME = credentials('sauce-username')
        SAUCE_ACCESS_KEY = credentials('sauce-access-key')
    }

    stages {
        stage('Run Sauce Labs Test') {
            steps {
                echo "Running on ${params.SIMULATOR} with Android ${params.ANDROID_VERSION}"

                // Bridge params to actual shell environment variables
                withEnv([
                    "EMULATOR=${params.SIMULATOR}",
                    "ANDROID_VERSION=${params.ANDROID_VERSION}"
                ]) {
                    sh 'npm install saucectl'
                    sh 'npx saucectl run'
                }
            }
        }
    }
}