pipeline {
    agent any

    tools {
        // This must match the name you gave Maven in 'Manage Jenkins > Tools'
        maven 'maven3'
    }

    stages {
        stage('Cleanup') {
            steps {
                // Cleans previous builds to save disk space on your EC2
                sh 'mvn clean'
            }
        }

        stage('Build & Package') {
            steps {
                // Compiles your code and creates the .war file in the target folder
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                // This uses the "Deploy to container" plugin
                // 'tomcat-credentials' is the ID you created in Jenkins Credentials
                deploy adapters: [tomcat9(url: 'http://localhost:8081', credentialsId: 'tomcat-credentials')], 
                       contextPath: 'typing-game', 
                       war: 'target/*.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful! Access at http://YOUR_IP:8081/typing-game/'
        }
        failure {
            echo 'Build failed. Check the Console Output for errors.'
        }
    }
}
