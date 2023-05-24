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
                    ls;
                    pwd;
                    call activate.bat
                    pip install -r requirements.txt;
                    pip install pytest pytest-cov;'''
            }
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
        stage('Lint with Pylint') {
            steps {
                script {
                    sh '''
                    .\\env\\Scripts\\activate.bat
                    pylint **/*.py
                    '''
                }
            }
        }
    }
}