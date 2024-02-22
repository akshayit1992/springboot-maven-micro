pipeline {
  agent any
  stages {
    stage('Checkout Scm') {
      steps {
        git(credentialsId: 'akshaygithub', url: 'https://github.com/akshayit1992/springboot-maven-micro.git')
      }
    }

    stage('Batch script 0') {
      steps {
        bat '''mvn package
'''
      }
    }

    stage('Batch script 1') {
      steps {
        bat 'mvn test'
      }
    }

    stage('No Converter-0') {
      steps {
        echo 'No converter for Builder: hudson.plugins.sonar.SonarRunnerBuilder'
      }
    }

  }
  post {
    always {
      step(checksName: '', $class: 'JUnitResultArchiver', testResults: 'target\\surefire-reports\\*.xml', stdioRetention: 'ALL')
    }

  }
  triggers {
    pollSCM('* * * * *')
  }
}
