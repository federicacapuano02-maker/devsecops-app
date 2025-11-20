pipeline {
    agent {
        docker {
            image 'python:3.11'
        }
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Clonazione repository completata'
            }
        }

        stage('Install dependencies') {
            steps {
                sh 'pip install --upgrade pip'
                sh 'if [ -f requirements.txt ]; then pip install -r requirements.txt; fi'
            }
        }

        stage('Run app') {
            steps {
                sh 'python app.py'
            }
        }

        stage('SAST - Snyk') {
    steps {
        withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
            sh '''
                pip install snyk
                snyk auth $SNYK_TOKEN
                snyk test || true
            '''
        }
    }
}

    }
}
