#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        jdk 'openjdk-15.0.2'
    }
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
                withGradle {
                    sh './gradlew test'
                }
            }
            post {
                script {
                    allure([
                        includeProperties: false,
                        jdk: 'openjdk-15.0.2',
                        properties: [],
                        reportBuildPolicy: 'ALWAYS',
                        results: [[path: 'build/allure-results']]
                ])
            }
        }
    }
}
