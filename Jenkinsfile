pipeline {
    agent any

    environment {
        // Limits Maven memory to prevent the EC2 instance from freezing
        MAVEN_OPTS = "-Xms128m -Xmx300m"
    }

    stages {
        stage('Checkout') {
            steps {
                // Jenkins automatically pulls the latest code from your GitHub
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // We use 'package' instead of 'clean package' to avoid the 
                // permission locks on the target folder
                sh 'mvn package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                // Moves the generated WAR file to Tomcat's webapps directory
                sh 'sudo cp target/typing-game.war /opt/tomcat9/webapps/'
                
                // Forces Tomcat to notice the new file immediately
                sh 'sudo touch /opt/tomcat9/webapps/typing-game.war'
            }
        }
    }

    post {
        success {
            echo 'Deployment successful! Check http://13.60.185.128:8081/typing-game/'
        }
        failure {
            echo 'Build failed. Check the Console Output for permission or memory errors.'
        }
    }
}
