pipeline {
    agent any

    tools {
        maven 'mavenwh'
        jdk 'jdkwh'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/walidevish/walidwh-app.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar -Dsonar.projectKey=walidwh-app'
                }
            }
        }

        stage('Docker Build') {
            steps {
                bat 'docker build -t walidwh-app .'
            }
        }
    }
}
