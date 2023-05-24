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
                sh '''python -m venv .venv;
                    cd .venv/Scripts;
                    ./activate.bat;
                    cd ..;
                    cd ..;
                    pwd;
                    python -m pip install -r requirements.txt;
                    python -m pip install pylint;
                    python -m pip install pytest pytest-cov;
                    '''
            }
        }

        stage('Static anal'){
            steps{
                sh 'python -m pylint ./sources/calc.py'
            }
        }

        stage('Run tests') {
            steps {

                sh '''
                    python -m pytest;
                    '''
            }
        }

        stage('Coverage report') {
            steps {
                sh 'python -m pytest --cov=sources --cov-report=html:coverage'
            }
        }

        stage('Archive coverage report') {
            steps {
                archiveArtifacts artifacts: 'coverage/*', onlyIfSuccessful: true
            }
        }
    }
}