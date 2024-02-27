pipeline {
    agent any

    environment {
        SONAR_TOKEN = credentials('sonarqjenkins')
    }

    stages {
        stage('Checkout Scm') {
            steps {
                git(credentialsId: 'akshaygithub', url: 'https://github.com/akshayit1992/springboot-maven-micro.git')
            }
        }

        stage('Batch script 0') {
            steps {
                bat 'mvn package'
            }
        }

        stage('Batch script 1') {
            steps {
                bat 'mvn test'
            }
        }

        stage('SonarCloud Analysis') {
            steps {
                // Execute SonarCloud scanner
               withSonarQubeEnv(credentialsId: 'sonarqjenkins', installationName: 'akshaysonarq') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            step(checksName: '', $class: 'JUnitResultArchiver', testResults: 'target\\surefire-reports\\*.xml', stdioRetention: 'ALL')
            // Publish quality gate result to Jenkins
            publishQualityGate()
        }
    }

    triggers {
        pollSCM('* * * * *')
    }
}
