#!/usr/bin/env groovy

BROWSER_LIST = ['firefox', 'chrome', 'opera']

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
                multiple_tests(BROWSER_LIST)
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

//@NonCPS
def multiple_tests(list) {
    for (int i = 0; i < list.size(); i++) {
        withGradle {
            sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${list[i]} -Pheadless=${HEADLESS_VALUE}'
        }
    }
/*
    list.each { each ->
        withGradle {
            sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${each} -Pheadless=${HEADLESS_VALUE}'
        }
    }
*/    
}
