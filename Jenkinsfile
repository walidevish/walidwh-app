pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/walidevish/walidwh-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=walidwh-app'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t walidwh-app .'
            }
        }
    }
}
