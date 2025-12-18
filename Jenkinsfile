pipeline {
    agent any

    tools {
        maven 'mavenwh'
        jdk 'jdkwh'
    }

    stage('Checkout') {
    steps {
        git branch: 'main', url: 'https://github.com/walidevish/walidwh-app.git', tool: 'gitwh'
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
