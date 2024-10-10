pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t flask-hello-world .'
            }
        }
        stage('Test') {
            steps {
                sh 'docker run -d --name flask-app -p 5000:5000 flask-hello-world'
                sh 'sleep 5'
                sh 'curl http://localhost:5000'
                sh 'docker stop flask-app'
                sh 'docker rm flask-app'
            }
        }
    }
}