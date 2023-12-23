pipeline {
    agent {
        docker {
            image 'python:3.10.3-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'sudo -H pip install -r requirements.txt'
            }
        }
        stage('Test') { 
            steps {
                echo 'Sudah ditahap test!'
            }
        }
    }
}