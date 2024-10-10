pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Run') {
            steps {
                bat 'python app.py'
            }
        }
    }
}