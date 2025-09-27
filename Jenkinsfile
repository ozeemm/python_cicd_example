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
                bat '''
                    python -m venv venv
                    . venv/Scripts/activate.exe
                    pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                bat '''
                    . venv/Scripts/activate.exe
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                bat 'pylint *.py'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m pytest tests/'
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