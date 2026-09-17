pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Récupération du code depuis GitHub...'
                checkout scm
            }
        }

        stage('Install dependencies') {
            steps {
                echo 'Installation des dépendances Python...'
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Unit Tests') {
            steps {
                echo 'Exécution des tests...'
                sh './venv/bin/python -m pytest'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline réussi !'
        }
        failure {
            echo '❌ Pipeline échoué.'
        }
    }
}