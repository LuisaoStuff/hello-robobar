#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {
	SERVER = 'http://10.250.5.20:4444'
	BROWSER_LIST = ['firefox', 'chrome', 'opera']
        BROWSER = 'firefox'
        HEADLESS_VALUE = 'false'
    }
    @NonCPS
    def multiple_tests(list) {
        list.each { each ->
            withGradle {
                sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${each} -Pheadless=${HEADLESS_VALUE}'
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
