pipeline {
    agent any

    tools {
        jdk 'java17'
        maven 'Maven3'   // match the exact name from Jenkins Global Tool Config
    }

    environment {
        // SONARQUBE SERVER NAME must match Jenkins "Configure System" > SonarQube installations
        SONARQUBE_SERVER = 'MySonarQube'
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
                withSonarQubeEnv('jenkins-sonarqube') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
