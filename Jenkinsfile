#!/usr/bin/env groovy
pipeline {
        agent any
    options {
        ansiColor('xterm')
    }
    environment {
        HEADLESS_VALUE = 'false'
        BROWSER = 'firefox'        
    }
    stages {
        stage('Test') {
            steps {
                script {
                    //sh "sed '/systemProperties\[\"selenide\.remote\"\]\ =\ \"http:\/\/10\.250\.5\.20:4444\"/d' build.gradle"
                    //sh "sed -e '/systemProperties\[\"selenide\.remote\"\]\ =\ "http:\/\/10\.250\.5\.20:4444\"/ s/^${LOCAL}*/${LOCAL}/' -i build.gradle"
                    sh "sed -i 's/firefox/${BROWSER}/g' build.gradle"
                    sh "sed -i 's/false/${HEADLESS_VALUE}/g' build.gradle"
                }
                withGradle {
                    sh './gradlew test'
//                    sh './gradlew iT'
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
