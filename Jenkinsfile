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
                sh '''
                    echo "Python location: $(which python3)"
                    echo "Python version: $(python3 --version)"
            
                    # Create venv safely
                    /usr/local/bin/python3 -m venv --without-pip venv
            
                    # Manually bootstrap pip inside venv
                    /usr/local/bin/python3 -m ensurepip --upgrade
            
                    # Activate and install requirements
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt || true
                    '''
            }
            }



        stage('Run Tests') {
            steps {
                sh '. venv/bin/activate && pytest'
            }
        }
    }
}
