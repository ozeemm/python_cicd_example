pipeline{
    agent any

    tools {
        python "Python39"
    }

    stages{
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                bat 'pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                bat './.venv/Scripts/pylint *.py'
            }
        }

        stage('Test') {
            steps {
                bat './.venv/Scripts/python -m pytest tests'
            }
        }

    }

    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}