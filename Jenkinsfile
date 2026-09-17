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

        stage('SAST - Bandit') {
            steps {
                echo 'Analyse statique de sécurité du code avec Bandit...'
                sh './venv/bin/pip install bandit'
                sh './venv/bin/bandit -r . -x ./venv -f txt'
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