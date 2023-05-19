pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SarGentle/simple-python-pyinstaller-app.git'
            }
        }

        stage('Setup environment') {
            steps {
                bat 'python -m venv .venv'
                bat '.venv/bin/pip install -r requirements.txt'
                bat '.venv/bin/pip install pytest pytest-cov'
            }
        }

        stage('Run tests') {
            steps {
                bat '.venv/bin/pytest'
            }
        }

        stage('Coverage report') {
            steps {
                bat '.venv/bin/pytest --cov=sources --cov-report=html:coverage'
            }
        }

        stage('Archive coverage report') {
            steps {
                archiveArtifacts artifacts: 'coverage/*', onlyIfSuccessful: true
            }
        }
    }
}