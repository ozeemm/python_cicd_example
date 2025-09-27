pipeline{
    agent any

    stages{
        stage('requirments'){
            sh 'pip install -r requirments.txt'
        }

        stage('tests'){
            sh 'pytest tests.py'
        }
    }
}