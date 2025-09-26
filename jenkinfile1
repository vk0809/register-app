pipeline {
    agent any

    tools {
        jdk 'java17'
        maven 'Maven3'   // match the exact name from Jenkins Global Tool Config
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
    }
}
