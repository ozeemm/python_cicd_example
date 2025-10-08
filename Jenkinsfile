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
                sh '''
                    python3 -m venv .venv
                    .venv/bin/python -m pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '.venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Lint') {
            steps {
                sh '.venv/bin/pylint *.py'
            }
        }

        stage('Tests') {
            steps {
                sh '.venv/bin/python -m pytest tests.py'
            }
        }

        stage('Run'){
            steps {
                sh '.venv/bin/python -m main.py'
            }
        }
    }
}