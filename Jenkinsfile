pipeline {
    agent any
    environment {
        MAVEN_OPTS = "-Xmx300m"
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy') {
            steps {
                // This automates the manual 'cp' command we did earlier
                sh 'sudo cp target/typing-game.war /opt/tomcat9/webapps/'
                // Optional: Force Tomcat to refresh
                sh 'sudo touch /opt/tomcat9/webapps/typing-game.war'
            }
        }
    }
}
