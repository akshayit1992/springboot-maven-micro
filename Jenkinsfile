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
    withSonarQubeEnv(credentialsId: 'sonarqjenkins', installationName: 'akshaysonarq') {
      bat "sonar-scanner -Dsonar.projectKey=akshayit1992_springboot-maven-micro -Dsonar.sources=src"

                }
            }
        }
    }

  

    triggers {
        pollSCM('* * * * *')
    }
}
