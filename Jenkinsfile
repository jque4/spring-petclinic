pipeline {
    agent any

    tools {
        maven 'MAVEN3'
        jdk 'JDK'
    }

    triggers {
        cron('H/10 * * * 1')
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/jque4/spring-petclinic.git', branch: 'main'
            }
        }

        stage('Build and Test') {
            steps {
                script {
                    withMaven(jdk: 'JDK', maven: 'MAVEN3') {
                        bat 'mvn clean compile verify'
                    }
                }
            }
        }

        stage('Jacoco Code Coverage') {
            steps {
                script {
                    jacoco(execPattern: '**/target/jacoco.exec')
                }
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }
}
