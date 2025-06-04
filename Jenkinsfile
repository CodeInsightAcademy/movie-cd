pipeline {
    agent any

    environment {
        APP_PORT = '5000'
        VENV_DIR = 'venv'
    }

    stages {
        stage('Checkout Code') {
            steps {                
                git url: 'git@github.com:CodeInsightAcademy/movie-cd.git', branch: 'master'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                python3 -m venv ${VENV_DIR}
                source ${VENV_DIR}/bin/activate
                pip install -r requirements.txt
                '''
            }
        }

        stage('Run Tests') {
            steps {
                sh '''
                source ${VENV_DIR}/bin/activate
                pytest
                '''
            }
        }

        stage('Deploy App') {
            steps {
                sh '''
                source ${VENV_DIR}/bin/activate
                nohup python3 app.py > flask.log 2>&1 &
                '''
            }
        }
    }

    post {
        failure {
            echo 'Deployment failed.'
        }
        success {
            echo 'Deployed successfully.'
        }
    }
}
