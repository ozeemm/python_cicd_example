pipeline{
    agent any

    stages{
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                bat  '''
                    python -m venv .venv
                    .venv\\Scripts\\python -m pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                bat '.venv\\Scripts\\pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                bat '.venv\\Scripts\\pylint *.py'
            }
        }

        stage('Tests') {
            steps {
                bat '.venv\\Scripts\\python -m pytest tests.py'
            }
        }

    }
}