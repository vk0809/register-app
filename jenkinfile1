pipeline {
    agent any

    tools {
        jdk 'java17'       // must match name in Jenkins Global Tool Config
        maven 'maven3'     // must match name in Jenkins Global Tool Config
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
