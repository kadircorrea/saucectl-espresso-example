pipeline {
  agent any

  parameters {
    // Dynamic parameters for devices
    string(name: 'ANDROID_VERSION', defaultValue: '15.0')
    string(name: 'SIMULATOR', defaultValue: 'Generic Medium Phone Emulator')
    
    // Retry and Threshold parameters
    string(name: 'RETRIES', defaultValue: '1', description: 'Global retries for the sauce session')
    string(name: 'PASS_THRESHOLD', defaultValue: '1', description: 'Number of passed attempts required to mark the suite as passed')
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
        echo "Configuring: ${params.SIMULATOR} (v${params.ANDROID_VERSION})"
        echo "Execution: Retries=${params.RETRIES}, Pass Threshold=${params.PASS_THRESHOLD}"

        // Export all variables for YAML expansion
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
}