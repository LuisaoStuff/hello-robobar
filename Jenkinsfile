#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
                withGradle {
//                    sh './gradlew test'
                    sh './gradlew iT'
//                    sh './gradlew codenarcTest'
                }
            }
            post {
                always {
                    junit 'build/test-results/**/TEST-*.xml'
/*                    publishHTML (target : [allowMissing: false,
                        alwaysLinkToLastBuild: true,
                        keepAll: true,
                        reportDir: 'build/reports/codenarc',
                        reportFiles: '*.html',
                        reportName: 'Reportes',
                        ])
*/                        
               }
            }
        }
    }
}
