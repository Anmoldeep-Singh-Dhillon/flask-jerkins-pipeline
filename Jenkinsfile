pipeline{
    agent{
        docker {
            image 'python:3.9'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }

    stages{
        stage('Checkout'){
            steps{
                git branch: 'main',url: 'https://github.com/Anmoldeep-Singh-Dhillon/flask-jerkins-pipeline.git'
            }
        }
        stage('Install dependencies'){
            steps{
                sh 'python3 -m venv venv'
                sh '. venv/bin/activate && pip install -r requirements.txt'            
                }
        }
        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest'
            }
        }
    }
}