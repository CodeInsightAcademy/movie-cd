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
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }
        stage('Run Tests') {
            steps {
                sh '''#!/bin/bash
                source venv/bin/activate
                pytest
                '''
            }
        }

        

        stage('Deploy App') {
            steps {
                sh '''
                    #!/bin/bash
                    source venv/bin/activate
                    python app.py
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
