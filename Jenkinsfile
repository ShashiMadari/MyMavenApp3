pipeline {
    agent any

    tools {
        // Ensure these tools are configured in Jenkins Global Tool Configuration
        gradle 'Gradle'     // Name of Gradle installation
                 // Name of JDK installation
    }

    environment {
        GRADLE_OPTS = "-Dorg.gradle.daemon=false"
    }

    stages {
        stage('Checkout') {
            steps {
                // Replace with your GitHub repo URL and branch if needed
                git branch: 'master', url: 'https://github.com/ShashiMadari/MyMavenApp3.git'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Build and tests succeeded.'
        }
        failure {
            echo 'Build or tests failed.'
        }
    }
}
