pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                url: 'https://github.com/SK-Tamil/jenkinsWithintegrateGithub.git'
            }
        }

        stage('Build') {
            steps {
                sh '''
                python3 -m venv venv
                . venv/bin/activate
                pip install --upgrade pip
                pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                . venv/bin/activate
                pytest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pkill -f gunicorn || true

                nohup venv/bin/gunicorn \
                -w 4 \
                -b 0.0.0.0:5000 \
                app:app > app.log 2>&1 &
                '''
            }
        }
    }
}
