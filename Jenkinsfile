pipeline {
    agent any

    tools {
        jdk 'JDK17'
        maven 'MAVEN3.9'
    }

    stages {

        stage('Checkout Code') {
            steps {
                git 'https://github.com/tirthmodi2904/simple-java-ci.git'
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
    }

    post {
        success {
            echo 'Build and Test completed successfully!'
        }
        failure {
            echo 'Build or Test failed!'
        }
    }
}
