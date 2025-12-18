pipeline {
    agent any

    tools {
        maven 'mavenwh'   // Make sure this matches the Maven tool name you configured
        jdk 'jdkwh'       // Make sure this matches the JDK name
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
                withSonarQubeEnv('walidwh') {  // Name of your SonarQube server configured in Jenkins
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t walidwh-app .'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
