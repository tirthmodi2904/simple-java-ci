pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'MAVEN3.9'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/tirthmodi2904/simple-java-ci.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('sonarserver') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        success {
            echo 'Build, Test & SonarQube analysis successful!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
