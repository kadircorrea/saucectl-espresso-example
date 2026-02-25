pipeline {
    agent any

    parameters {
        // Your existing dynamic parameters
        string(name: 'ANDROID_VERSION', defaultValue: '15.0')
        string(name: 'SIMULATOR', defaultValue: 'Generic Medium Phone Emulator')
        
        // The new Retries field with a default of 1
        string(name: 'RETRIES', defaultValue: '1', description: 'Number of times to retry failed test cases')
    }

    environment {
        SAUCE_USERNAME = credentials('sauce-username')
        SAUCE_ACCESS_KEY = credentials('sauce-access-key')
    }

    stages {
        stage('Initialize') {
            steps {
                cleanWs()
            }
        }

        stage('Run Sauce Labs Test') {
            steps {
                withEnv([
                    "EMULATOR=${params.SIMULATOR}",
                    "ANDROID_VERSION=${params.ANDROID_VERSION}"
                ]) {
                    sh 'npm install saucectl'
                    
                    sh "npx saucectl run --retries ${params.RETRIES}"
                }
            }
        }
    }
}