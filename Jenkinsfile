pipeline {
    agent { label 'isl' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '15'))
    }
    tools {
        jdk 'JDK 1.8'
    }
    stages {
        stage('Gradle build') {
            steps {
                withCredentials([string(credentialsId: 'cdd_artifactory_password', variable: 'ARTIFACTORY_PASSWORD')]) {
                    sh """./gradlew build uploadArchives \
                    -xtest \
                    -Partifactory_username=bldcddbuild.co \
                    -Partifactory_password=$ARTIFACTORY_PASSWORD"""
                }
            }
        }
    }
}