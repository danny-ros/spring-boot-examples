pipeline {
  agent {
    node {
      label 'CentOS7'
    }

  }
  stages {
    stage('checkout code') {
      steps {
        git(branch: 'danny_sol', url: 'https://github.com/danny-ros/spring-boot-examples.git')
      }
    }

    stage('Build') {
      steps {
        sh '''cd spring-boot-package-war
		mvn compile'''
      }
    }

    stage('Test') {
      post {
        always {
          junit '**/surefire-reports/**/*.xml'
        }

      }
      steps {
        sh '''cd spring-boot-package-war
				mvn test'''
      }
    }

    stage('Deploy to Integration ') {
      steps {
        sh '''cd spring-boot-package-war
				mvn build-helper:parse-version versions:set -DnewVersion=0.0.2.$BUILD_ID-SNAPSHOT versions:commit
				mvn package'''
      }
    }

    stage('Artifacts') {
      steps {
        archiveArtifacts 'spring-boot-package-war/target/*.war'
      }
    }

    stage('slack') {
      steps {
        slackSend(channel: 'danny-dev', color: '#439FE0', message: 'new mvn build', tokenCredentialId: 'Slack')
      }
    }

  }
}
