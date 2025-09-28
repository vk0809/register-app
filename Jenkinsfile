pipeline {
    agent any

    tools {
        jdk 'java17'
        maven 'Maven3'
    }

    environment {
        SONARQUBE_SERVER = 'MySonarQube' // Jenkins SonarQube server name
    }

    stages {
        stage('Check Java & Maven') {
            steps {
                sh 'java -version'
                sh 'mvn -v'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    withSonarQubeEnv(SONARQUBE_SERVER) {
                        sh 'mvn sonar:sonar'
                    }
                }
            }
        }
    }
}
