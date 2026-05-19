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
               sh 'python3 -m pip install -r requirements.txt'
            }
        }

        stage('Test') {
            steps {
                sh 'pytest'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                pkill -f "gunicorn" || true
                nohup gunicorn -w 4 -b 0.0.0.0:5000 app:app > app.log 2>&1 &
                '''
            }
        }
    }
}
