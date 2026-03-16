pipeline {
    agent any

    stages {

          stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/cavillaz/proyecto-laravel-docker.git'
            }
        }

        stage('Detect Changes') {
            steps {
                sh 'ls -la'
            }
        }

        stage('Build Containers') {
            steps {
                sh 'docker compose -f docker-compose.yaml build'
            }
        }

        stage('Start Containers') {
            steps {
                sh 'docker compose -f docker-compose.yaml up -d'
            }
        }

        stage('Install Laravel Dependencies') {
            steps {
                sh 'docker compose exec -T app composer install'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'docker compose exec -T app php artisan migrate --force'
            }
        }

    }
}