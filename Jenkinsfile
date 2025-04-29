pipeline {
    agent any

    tools {
        gradle 'Gradle'  // Make sure this matches the tool name in Jenkins Global Tool Config
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/ShashiMadari/MyMavenApp3.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    sh 'chmod +x ./gradlew'               // Ensure gradlew is executable
                    sh './gradlew clean build --info --stacktrace'
                }
            }
        }

        stage('Run JAR') {
            steps {
                script {
                    def jarFiles = sh(script: 'ls build/libs/*.jar', returnStdout: true).trim().split('\n')
                    if (jarFiles.length == 0) {
                        error('No JAR file found in build/libs.')
                    }
                    sh "java -jar ${jarFiles[0]}"
                }
            }
        }
    }

    post {
        success {
            echo 'Gradle build and JAR run completed successfully!'
        }
        failure {
            echo 'Gradle build or execution failed.'
        }
    }
}
