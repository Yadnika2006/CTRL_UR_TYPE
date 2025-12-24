pipeline {
    agent any
    tools {
        maven 'maven3'
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                // 'tomcat-credentials' must be created in Jenkins Credentials
                deploy adapters: [tomcat9(url: 'http://localhost:8081', credentialsId: 'tomcat-credentials')], 
                       contextPath: 'typing-game', 
                       war: 'target/*.war'
            }
        }
    }
}
