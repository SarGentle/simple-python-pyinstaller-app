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
                sh 'python -m venv .venv'
                sh 'cd .venv/Scripts'
                sh 'ls'
                sh 'activate.bat'
                sh 'pip install -r requirements.txt'
                sh 'pip install pytest pytest-cov'
            }
        }

        stage('Run tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Coverage report') {
            steps {
                sh 'pytest --cov=sources --cov-report=html:coverage'
            }
        }

        stage('Archive coverage report') {
            steps {
                archiveArtifacts artifacts: 'coverage/*', onlyIfSuccessful: true
            }
        }
    }
}