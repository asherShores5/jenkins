pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker build -t my-flask-app .'
            }
        }
        
        stage('Test') {
            steps {
                sh 'docker run --rm my-flask-app python -m unittest discover tests'
            }
        }
        
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 5000:5000 my-flask-app'
            }
        }
    }
    
    post {
        always {
            sh 'docker system prune -f'
        }
    }
}