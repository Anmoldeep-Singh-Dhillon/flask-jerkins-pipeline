pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Anmoldeep-Singh-Dhillon/flask-jerkins-pipeline.git'
            }
        }

        stage('Install dependencies') {
            steps {
                sh '/usr/local/bin/python3 -m venv venv'
                sh '. venv/bin/activate && /usr/local/bin/pip3 install -r requirements.txt'
            }
        }


        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest'
            }
        }
    }
}
