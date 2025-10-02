pipeline {
    agent any

    tools {
        jdk 'java17'          // This must match the JDK name in Jenkins Global Tool Config
        maven 'Maven3'        // This must match the Maven installation name in Jenkins Global Tool Config
    }

    environment {
        // Example: set artifact name or environment vars
        APP_NAME = "my-app"
    }

    stages {
        stage('Check Java & Maven Versions') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-repo/your-project.git'
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
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying ${APP_NAME}..."
                // Example deploy step, replace with your own (Docker, SSH, k8s, etc.)
                sh 'echo "Deployment step goes here"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check logs.'
        }
    }
}
