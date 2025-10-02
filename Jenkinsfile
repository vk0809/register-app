pipeline {
    agent any

    tools {
        jdk 'java17'          // Must match Jenkins Global Tool Config
        maven 'Maven3'        // Must match Jenkins Global Tool Config
    }

    environment {
        APP_NAME = "my-app"
    }

    stages {
        stage('Check Java & Maven Versions') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
            post {
                success {
                    // Archive jars from any module (avoids earlier error)
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying ${APP_NAME}..."
                sh 'echo "Deployment step goes here"'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Please check logs.'
        }
    }
}
