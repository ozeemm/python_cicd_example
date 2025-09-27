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
                    python -m venv venv
                    . venv/Scripts/activate.exe
                    pip install --upgrade pip
                '''
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh '''
                    . venv/Scripts/activate.exe
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Lint') {
            steps {
                sh 'pylint *.py'
            }
        }

        stage('Test') {
            steps {
                sh 'python -m pytest tests/'
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