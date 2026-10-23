pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    python3 -m venv .venv
                    .venv/bin/pip install -q -r requirements.txt pytest
                '''
            }
        }
    
    stage('Seguridad') {
        steps {
            sh 'bandit -ll app.py'
            sh 'pip-audit -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh '.venv/bin/python -m pytest -q'
            }
        }

        stage('Deploy') {
            steps {
                sh 'bash deploy.sh'
            }
        }
    }
}
