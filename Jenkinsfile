pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java21'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/Kunal-18L/java-maven-webapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQUbeEnv('sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
