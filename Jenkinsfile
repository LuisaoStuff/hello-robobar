#!/usr/bin/env groovy
pipeline {
        agent any
    options {
        ansiColor('xterm')
    }
    environment {
	SERVER = 'http://10.250.5.20:4444'
        BROWSER = 'firefox'
        HEADLESS_VALUE = 'false'
    }
    stages {
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${BROWSER} -Pheadless=${HEADLESS_VALUE}'
                }
            }
            post {
                always {
                    junit 'build/test-results/**/TEST-*.xml'
               }
            }
        }
    }
}
