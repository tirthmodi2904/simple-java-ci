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
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    sh """
                    mvn sonar:sonar \
                      -Dsonar.host.url=http://172.31.18.31:9000 \
                      -Dsonar.login=$SONAR_TOKEN
                    """
                }
            }
        }

        stage('Upload Artifact to Nexus') {
    steps {
        withCredentials([usernamePassword(
            credentialsId: 'nexuslogin',
            usernameVariable: 'NEXUS_USER',
            passwordVariable: 'NEXUS_PASS'
        )]) {
            sh """
            mvn deploy -DskipTests -s /var/lib/jenkins/.m2/settings.xml
            """
        }
    }
}

    }

    post {
        success {
            echo 'Build, Test, SonarQube & Nexus upload SUCCESS!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
