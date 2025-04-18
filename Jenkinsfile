pipeline {
    
	agent any
    tools {
	    maven "maven3"
	    jdk "java17"
	}
	
    stages{
        
        stage ('fetch code') {
            steps {
                git branch: 'java', url: 'https://github.com/HuseyinBeller/sonarqube-jenkins.git'
            }
        }
        stage('build-app'){
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('app-compile'){
            steps {
                sh 'mvn clean compile -DskipTests'
            }
        }

        stage('code analysis with sonarqube') {
          
		  environment {
             scannerHome = tool 'sonar-scanner-6'
          }
          steps {
            withSonarQubeEnv('sonar-server') {
               sh '''${scannerHome}/bin/sonar-scanner \
                   -Dsonar.projectKey=curtis-java-app \
                   -Dsonar.projectName=curtis-java-app \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/main/java \
                   -Dsonar.java.binaries=target/classes \
                   -Dsonar.organization=curtis-org'''
            }
          }
        }
    }
}
