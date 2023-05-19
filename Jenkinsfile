pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/SarGentle/simple-python-pyinstaller-app.git'
            }
        }

        stage('Install dependencies') {
            steps {
                // Install required Python packages
                bat 'python -m pip install pytest pytest-cov'
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