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
        }
        stage('Deploy to Integration ') {
            steps {
                sh 'cp "/opt/tomcat/.jenkins/workspace/spring-boot-examples/target/spring-boot-package-war-0.0.1-SNAPSHOT.war" /opt/tomcat/latest/webapps/spring-boot-package-war-0.0.${BUILD_ID}-SNAPSHOT.war'
            }
        }
		stage('packege  {mvn clean packege}') {
		  steps {
			sh '''cd spring-boot-package-war  
			mvn clean package'''
      }
    }
    }   
}
