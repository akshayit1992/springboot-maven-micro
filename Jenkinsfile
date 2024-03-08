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
               withSonarQubeEnv(credentialsId: 'sonartk', installationName: 'akshaysonarq') {
                   bat mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar -Dsonar.projectKey=demo1992_mydemo
                    // bat 'sonar-scanner sonar-project.properties'
                }
            }
        }
    }



    triggers {
        pollSCM('* * * * *')
    }
}
