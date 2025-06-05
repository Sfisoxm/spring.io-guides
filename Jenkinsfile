pipeline {
    agent any
    
    stages {
        stage('Install Maven') {
            steps {
                script {
                    echo 'Installing Apache Maven...'
                    
                    bat '''
                        @echo off
                        set MAVEN_VERSION=3.9.9
                        set MAVEN_URL=https://archive.apache.org/dist/maven/maven-3/3.9.9/binaries/apache-maven-3.9.9-bin.zip
                        
                        echo Checking if Maven exists...
                        if exist "apache-maven-%MAVEN_VERSION%" (
                            echo Maven already installed
                        ) else (
                            echo Downloading Maven...
                            powershell -Command "Invoke-WebRequest -Uri '%MAVEN_URL%' -OutFile 'maven.zip'"
                            
                            echo Extracting Maven...
                            powershell -Command "Expand-Archive -Path 'maven.zip' -DestinationPath '.' -Force"
                            
                            echo Cleaning up...
                            del maven.zip
                            
                            echo Maven installation completed
                        )
                    '''
                }
            }
        }
        
        stage('Verify Installation') {
            steps {
                bat '''
                    set MAVEN_HOME=%WORKSPACE%\\apache-maven-3.9.9
                    set PATH=%MAVEN_HOME%\\bin;%PATH%
                    
                    echo Verifying Java...
                    java -version
                    
                    echo Verifying Maven...
                    mvn --version
                '''
            }
        }
        
        stage('Build Project') {
            steps {
                bat '''
                    set MAVEN_HOME=%WORKSPACE%\\apache-maven-3.9.9
                    set PATH=%MAVEN_HOME%\\bin;%PATH%
                    
                    echo Starting Maven build...
                    mvn clean compile test package
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Build process completed'
        }
    }
}
