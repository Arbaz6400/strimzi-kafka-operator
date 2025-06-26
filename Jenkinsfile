
pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6'  // Set this name in Jenkins Global Tool Configuration
        jdk 'JDK 17'         // Set this name too
    }

    environment {
        MAVEN_OPTS = "-Dmaven.test.skip=true"
    }

    stages {
        stage('Checkout') {
            steps {
                // Automatically pulls from configured Git repo and branch
                checkout scm
            }
        }

        stage('Build Strimzi Kafka Operator') {
            steps {
                sh 'mvn clean install -B -DskipTests'
            }
        }

        stage('Archive JARs') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '✅ Strimzi Kafka Operator build successful!'
        }
        failure {
            echo '❌ Build failed. Please check logs.'
        }
    }
}
