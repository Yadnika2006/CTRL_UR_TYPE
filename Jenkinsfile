pipeline {
    agent any

    tools {
        // Must match the name you gave Maven in Global Tool Configuration
        maven 'maven3' 
    }

    stages {
        stage('Checkout') {
            steps {
                // Pulls code from your GitHub
                git branch: 'main', url: 'https://github.com/Yadnika2006/CTRL_UR_TYPE.git'
            }
        }

        stage('Build') {
            steps {
                // Compiles and creates the .war file
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                // Deploys the WAR to your running Tomcat
                deploy adapters: [tomcat9(url: 'http://localhost:8081', credentialsId: 'tomcat-credentials')], 
                       contextPath: 'typing-game', 
                       war: 'target/*.war'
            }
        }
    }
}
