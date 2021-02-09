#!/usr/bin/env groovy

pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('trivy') {
            steps {
                sh 'trivy fs --format json --output repo-sec.json .'
            }        
            post {
                always {
                    recordIssues enabledForFailure: true, tool: trivy(pattern: 'repo-sec.json')
                }
            }
        }
    }
}
