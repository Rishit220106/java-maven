pipeline {
    agent any

    tools {
        jdk 'JDK17'       // exact name from Global Tool Configuration
        maven 'maven'     // exact name from Global Tool Configuration
    }

    environment {
        SONARQUBE_SERVER = 'SonarQube-Docker'
        SONAR_TOKEN = credentials('sonar-token')  // stored Jenkins credential
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Rishit220106/java-maven.git'
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
                withSonarQubeEnv('SonarQube-Docker') {
                    sh "mvn sonar:sonar -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }
    }

    post {
        always {
            // Collect test reports
            junit '**/target/surefire-reports/*.xml'

            // Optional: Archive build artifacts
            archiveArtifacts artifacts: 'target/*.jar', allowEmptyArchive: true
        }
        success {
            echo 'Build, test, and SonarQube analysis completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check the logs above for details.'
        }
    }
}
