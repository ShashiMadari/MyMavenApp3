pipeline {
    agent any

    tools {
        gradle 'Gradle'  // Ensure Gradle is installed and configured in Jenkins (Global Tool Config)
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ShashiMadari/MyMavenApp3.git'
            }
        }

        stage('Init from POM (if needed)') {
            steps {
                sh 'gradle init --type pom'
            }
        }

        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    // Replace with your actual JAR name if needed
                    def jarFile = sh(script: "ls build/libs/*.jar", returnStdout: true).trim()
                    sh "java -jar ${jarFile}"
                }
            }
        }
    }

    post {
        success {
            echo 'Gradle build and run completed successfully!'
        }
        failure {
            echo 'Gradle build or execution failed.'
        }
    }
}
