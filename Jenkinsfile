pipeline {
    agent any
    tools {
        jdk 'JDK17'
        maven 'M3'
    }
    stages {
        stage('Checkout') { steps { checkout scm } }
        stage('Build') { steps { sh 'mvn clean package' } }
        stage('Test') {
            steps { sh 'mvn test' }
            post { always { junit 'target/surefire-reports/*.xml' } }
        }
        stage('Package') {
            steps { archiveArtifacts artifacts: 'target/*.jar', fingerprint: true }
        }
        stage('Deploy') {
            steps { sh 'java -jar target/my-java-app-1.0-SNAPSHOT.jar' }
        }
    }
}
