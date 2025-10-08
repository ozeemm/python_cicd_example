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
                    . .venv/bin/activate
                    pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '''
                    . .venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                sh '''
                    . .venv/bin/activate
                    pylint *.py
                '''
            }
        }

        stage('Tests') {
            steps {
                sh '''
                    . .venv/bin/activate
                    pytest tests.py
                '''
            }
        }

        stage('Run'){
            steps {
                sh '''
                    . .venv/bin/activate
                    python main.py
                '''
            }
        }
    }
}