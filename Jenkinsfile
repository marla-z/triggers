pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
        timestamps() 
    }
    environment {
        // Git
        repo = "https://github.com/marla-z/triggers.git"
        branch = "${env.Branch}"
        // Postgres
        pg_user = "vagrant"
        pg_pass = "vagrant"
        pg_db = "u_solutions_core_tests"
        pg_env = "-e POSTGRES_USER=${pg_user} -e POSTGRES_PASSWORD=${pg_pass} -e POSTGRES_DB=${pg_db}"
        // Docker images
        image_php = "u_solutions_core_php-8.1"
        image_postgres = "postgres:14"
    }
    stages {
        stage('Init') {
            steps {
                script {
                    pgBox = docker.image("${env.image_postgres}").withRun("${pg_env}")
                }
            }
        }

        stage('Checkout') {
            steps {
                script {
                    pgBox.inside() {
                        echo "21"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    echo "plug"
                }
            }
        }
    }
}