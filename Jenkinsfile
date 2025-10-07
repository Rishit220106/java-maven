pipeline {
    agent any
    tools {
        jdk 'JDK17'       // exact name of your JDK installation
        maven 'maven'     // exact name of your Maven installation
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Rishit220106/java-maven.git'
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
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
