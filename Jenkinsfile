pipeline {
    agent any

    tools {
        maven 'Maven 3.9.10'   // Update to match what's configured in Jenkins
        jdk 'JDK 17'           // Update this name if needed
    }

    environment {
        MAVEN_OPTS = "-Dmaven.test.skip=true"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Strimzi Kafka Operator') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Build completed successfully.'
        }
        failure {
            echo '❌ Build f
