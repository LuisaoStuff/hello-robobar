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
// Múltiples Pruebas
                multiple_tests()
                
/* Solo una prueba
                withGradle {
                    sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${BROWSER} -Pheadless=${HEADLESS_VALUE}'
                }
*/
            }
            post {
                always {
                    junit 'build/test-results/**/TEST-*.xml'
               }
            }
        }
    }
}

def multiple_tests() {
    withGradle {
        sh './gradlew test -Premote_server=${SERVER} -Pbrowser=firefox -Pheadless=${HEADLESS_VALUE}'
        sh './gradlew test -Premote_server=${SERVER} -Pbrowser=chrome -Pheadless=${HEADLESS_VALUE}'
        sh './gradlew test -Premote_server=${SERVER} -Pbrowser=opera -Pheadless=${HEADLESS_VALUE}'
    }
}
