#!/usr/bin/env groovy
pipeline {
variableReplace(
	configs: [
		variablesReplaceConfig(
			configs: [
				variablesReplaceItemConfig( 
					name: 'DATABASE_HOST',
					value: 'localhost'
				),
				variablesReplaceItemConfig( 
					name: 'DATABASE_NAME',
					value: 'my_db'
				),
				variablesReplaceItemConfig( 
					name: 'DATABASE_PORT',
					value: '3306'
				),
				variablesReplaceItemConfig( 
					name: 'DATABASE_PASSWORD',
					value: '123456'
				)
			],
			fileEncoding: 'UTF-8', 
			filePath: 'database-config.php', 
			variablesPrefix: '#{', 
			variablesSuffix: '}#'
            )]
)

    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Test') {
            steps {
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
