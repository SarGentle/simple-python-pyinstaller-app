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
                    python -m pip install pytest pytest-cov;
                    '''
            }
        }

        stage('Run tests') {
            steps {

                sh '''
                    cd .venv/Scripts;
                    cat activate;
                    . activate;
                    cd ../..;
                    pwd;
                    python -m pip -V;
                    python -m pip list;
                    pytest
                    '''
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