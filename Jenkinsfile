pipeline {
    agent any

    environment {
        // Java 17 configuration (Windows safe)
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-21.0.10"
        PATH = "${JAVA_HOME}\\bin;${env.PATH}"
    }

    tools {
        maven 'M3'   // Must match Global Tool Configuration name
    }

    stages {

        stage('Check Versions') {
            steps {
                bat 'java -version'
                bat 'mvn --version'
            }
        }

        stage('Get Code from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AaryaPatel1511/pipeline.git'
            }
        }

        stage('Build Project') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonar_si') {
                    bat 'mvn sonar:sonar'
                }
            }
        }
    }
}
