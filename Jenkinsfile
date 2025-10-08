pipeline{
    agent any

    environment {
        ACTIVATE_VENV_PATH = '.venv/bin/activate'
    }

    stages{
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Setup Virtual Environment') {
            steps {
                sh "
                    python3 -m venv .venv
                    source ${ACTIVATE_VENV_PATH}
                    pip install --upgrade pip
                "
            }
        }
        
        stage('Install Dependencies') {
            steps {
                sh "
                    source ${ACTIVATE_VENV_PATH}
                    pip install -r requirements.txt
                "
            }
        }

        stage('Lint') {
            steps {
                sh "
                    source ${ACTIVATE_VENV_PATH}
                    pylint *.py
                "
            }
        }

        stage('Tests') {
            steps {
                sh "
                    source ${ACTIVATE_VENV_PATH}
                    pytest tests.py
                "
            }
        }

        stage('Run'){
            steps {
                sh "
                    source ${ACTIVATE_VENV_PATH}
                    python main.py
                "
            }
        }
    }
}