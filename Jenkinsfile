pipeline {
    agent any
    
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3.9.9-eclipse-temurin-21-alpine'
                    // Use Unix-style path or let Jenkins handle it automatically
                    args '-v /var/run/docker.sock:/var/run/docker.sock'
                }
            }
            steps {
                // Your build steps here
                sh 'mvn --version'
                // Add your actual build commands
            }
        }
    }
}
