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
                powershell  '''
                    python -m venv .venv
                    .venv\\Scripts\\python -m pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                powershell '.venv\\Scripts\\pip install -r requirements.txt'     
            }
        }

        stage('Lint') {
            steps {
                powershell '.venv\\Scripts\\pylint *.py'
            }
        }

        stage('Test') {
            steps {
                powershell '.venv\\Scripts\\python -m pytest tests'
            }
        }

    }
}