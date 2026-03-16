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

        /* stage('Build Containers') {
            steps {
                sh 'docker ps'
            }
        } */

        stage('Start Containers') {
            steps {
                sh 'docker compose -f docker-compose.yaml up -d'
            }
        }

        /* stage('Build Containers') {
            steps {
                sh 'docker ps'
            }
        }
 */
        stage('Install Laravel Dependencies') {
            steps {
                sh 'docker compose exec -T app bash -c "cd /var/www && composer install"'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'docker compose exec -T app bash -c "cd /var/www && php artisan migrate --force"'
            }
        }

    }
}