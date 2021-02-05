#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
	SERVER = 'http://10.250.5.20:4444'
	BROWSER_LIST = [ 'firefox', 'chrome', 'opera']
        BROWSER = 'firefox'
        HEADLESS_VALUE = 'false'
    }
    multiple_tests(BROWSER_LIST) {
        BROWSER_LIST.each { EACH_BROWSER ->
            withGradle {
                sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${EACH_BROWSER} -Pheadless=${HEADLESS_VALUE}'
            }
        }
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
