pipeline {
    agent any

    tools {
        // Names must match the ones configured in Jenkins global tools
        maven 'maven'    // Maven installation name
        jdk 'JDK17'      // JDK installation name
    }

    environment {
        SONARQUBE = 'SonarQube-Docker' // SonarQube installation name in Jenkins
    }

    stages {

        stage('Checkout') {
            steps {
                // Replace with your GitHub repo URL
                git branch: 'main', url: 'https://github.com/Rishit220106/java-maven.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
                junit '**/target/surefire-reports/*.xml'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                // Runs Maven SonarQube analysis with the configured SonarQube environment
                withSonarQubeEnv(SONARQUBE) {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
        success {
            echo 'Build and analysis completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs!'
        }
    }
}
