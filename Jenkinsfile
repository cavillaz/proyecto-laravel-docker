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

     /*    stage('Stop Containers') {
            steps {
                sh 'docker compose down --remove-orphans'
            }
        } */

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
        
     /*    stage('Build Containers') {
            steps {
                sh 'docker ps'
            }
        } */
 
        stage('Install Laravel Dependencies') {
            steps {
                sh 'docker compose run --rm app composer install'
            }
        }

        stage('Run Migrations') {
            steps {
                sh 'docker compose run --rm app php artisan migrate --force'
            }
        }

    }
}