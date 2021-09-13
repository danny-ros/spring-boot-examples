pipeline {
    agent {
        label 'master'
    }
    stages{
        stage('checkout code'){
            steps {
                git branch: 'danny_sol', url: 'https://github.com/danny-ros/spring-boot-examples.git'
            }
        }
        stage('Build'){
            steps {
                sh '''cd spring-boot-package-war
		mvn compile'''
            }
        }
		stage('Test'){
            steps {
                sh '''cd spring-boot-package-war
				mvn test'''
            }
			post {
				always {
					junit '**/surefire-reports/**/*.xml'
				}
			}
        }
        stage('Deploy to Integration ') {
            steps {
                sh '''cd spring-boot-package-war
				mvn build-helper:parse-version versions:set -DnewVersion=0.0.$BUILD_ID-SNAPSHOT versions:commit'''
            }
        }
		stage('Artifacts') {
		  steps {
			archiveArtifacts artifacts: 'spring-boot-package-war/target/*.war', followSymlinks: false
      }
    }
    }   
}
