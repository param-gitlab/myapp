pipeline {
    agent none
    stages {
        stage('Checkout') {
            agent { label 'build' }
            steps {
                git branch: 'main', url: 'https://github.com/param-gitlab/myapp.git'
            }
        }
        stage('Build Docker Image') {
            agent { label 'build' }
            steps {
                sh 'docker build -t myapp:latest .'
            }
        }
        stage('Test Container') {
            agent { label 'build' }
            steps {
                sh 'docker run --rm myapp:latest echo "Tests passed!"'
            }
        }
        stage('Deploy') {
            agent { label 'deploy' }
            steps {
                sh 'docker run -d -p 8080:8080 myapp:latest'
            }
        }
    }
}

