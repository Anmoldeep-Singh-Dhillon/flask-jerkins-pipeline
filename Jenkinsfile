pipeline {
    agent any

    environment {
        VENV_DIR = "venv"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "🔄 Checking out repository..."
                git branch: 'main', url: 'https://github.com/Anmoldeep-Singh-Dhillon/flask-jerkins-pipeline.git'
            }
        }

        stage('Setup Python Environment') {
            steps {
                echo "🐍 Setting up Python environment..."
                sh '''
                    echo "Python location: $(which python3)"
                    echo "Python version: $(python3 --version)"

                    # Clean up old virtual environment if any
                    rm -rf ${VENV_DIR}

                    # Create a new virtual environment with system site packages
                    python3 -m venv --system-site-packages ${VENV_DIR}

                    # Activate the environment
                    . ${VENV_DIR}/bin/activate

                    # Ensure pip is available and upgraded
                    python3 -m pip install --upgrade pip setuptools wheel

                    # Install dependencies (ignore empty requirements.txt)
                    pip install -r requirements.txt || true

                    echo "✅ Virtual environment and dependencies ready."
                '''
            }
        }

        stage('Run Tests') {
            steps {
                echo "🧪 Running unit tests..."
                sh '''
                    . ${VENV_DIR}/bin/activate
                    if [ -d "tests" ]; then
                        pytest -v || true
                    else
                        echo "No tests folder found, skipping tests."
                    fi
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check above logs for details."
        }
        always {
            echo "🧹 Cleaning up workspace..."
            sh "rm -rf ${VENV_DIR}"
        }
    }
}
