#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    
    environment {
        def BROWSER_LIST = ['firefox', 'chrome', 'opera']
	    SERVER = 'http://10.250.5.20:4444'
        BROWSER = 'firefox'
        HEADLESS_VALUE = 'false'
    }
    stages {
        stage('Test') {
            steps {
// Múltiples Pruebas
//                multiple_tests(BROWSER_LIST)
                script {
                    for (int i = 0; i < BROWSER_LIST.size(); i++) {
                        withGradle {
                            sh './gradlew test -Premote_server=${SERVER} -Pbrowser=${BROWSER_LIST[i]} -Pheadless=${HEADLESS_VALUE}'
                        }
                    }
                }
                
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
