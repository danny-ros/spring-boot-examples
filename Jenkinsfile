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
        stage('Build and Test'){
            steps {
                sh '''cd spring-boot-package-war
		mvn package'''
            }
        }
		
        stage('Deploy to Integration ') {
            steps {
                sh 'cp "/opt/tomcat/.jenkins/workspace/final project/target/spring-boot-package-war-0.0.${BUILD_ID}-SNAPSHOT.war" /opt/tomcat/latest/webapps'
            }
        }
    }   
}
