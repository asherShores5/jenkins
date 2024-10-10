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
                script {
                    try {
                        sh 'docker build -t my-flask-app .'
                    } catch (err) {
                        echo "Docker build failed: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping early!")
                    }
                }
            }
        }
        
        stage('Test') {
            steps {
                script {
                    try {
                        sh 'docker run --rm my-flask-app python -m unittest discover tests'
                    } catch (err) {
                        echo "Tests failed: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping early!")
                    }
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    try {
                        sh 'docker stop my-flask-app || true'
                        sh 'docker rm my-flask-app || true'
                        sh 'docker run -d -p 5000:5000 --name my-flask-app my-flask-app'
                    } catch (err) {
                        echo "Deployment failed: ${err}"
                        currentBuild.result = 'FAILURE'
                        error("Stopping early!")
                    }
                }
            }
        }
    }
    
    post {
        always {
            sh 'docker system prune -f || true'
        }
    }
}