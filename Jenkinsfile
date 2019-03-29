pipeline {
    agent any
    tools {
        jdk 'jdk8'
//        maven 'maven3'
    }
    stages {
        stage('Install') {
            steps {
                sh "mvn clean test"
            }
            post {
                always {
                    junit '**/target/*-reports/TEST-*.xml'
                }
            }
        }
        stage('deploy') {
            steps {
                configFileProvider([configFile(fileId: 'our_settings', variable: 'SETTINGS')]) {
                    sh "mvn deploy  -DskipTests -Dnexus-releases-url=${env.NEXUS_RELEASES_URL} -Dnexus-snapshots-url=${env.NEXUS_SNAPSHOTS_URL}"
                }

            }
        }
    }
}