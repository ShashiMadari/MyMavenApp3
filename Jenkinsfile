pipeline {
    agent any

    tools {
        gradle 'Gradle'  // Ensure Gradle is installed and configured in Jenkins (Global Tool Config)
    }

    stages {
        stage('Checkout') {pipeline {
    agent any

    tools {
        gradle 'Gradle'  // Make sure this name matches Jenkins global tool config
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
                    // Ensure Gradle wrapper is executable
                    sh 'chmod +x ./gradlew'

                    // Run the build with more diagnostics
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
