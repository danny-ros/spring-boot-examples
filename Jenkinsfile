pipeline {
    agent {
        label 'master'
    }
    stages{
        stage('checkout code'){
            steps {
                git branch: 'IditOryDanny_2_sol', url: 'https://github.com/danny-ros/spring-boot-examples.git'
            }
        }
        stage('Build'){
            steps {
                sh '''cd spring-boot-package-war'''
				sh '''mvn compile'''
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
                sh 'cp "/opt/tomcat/.jenkins/workspace/final project/target/spring-boot-package-war-0.0.${BUILD_ID}-SNAPSHOT.war" /opt/tomcat/latest/webapps'
            }
        }
    }   
}
