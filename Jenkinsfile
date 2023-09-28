pipeline {
    agent { label 'runner' }

    options {
        ansiColor('xterm')
        timestamps() 
    }

    environment {
        // Git
        REPO = "https://github.com/marla-z/triggers.git"
        BRANCH = "${env.Branch}"
        // Postgres
        PG_USER = "vagrant"
        PG_PASS = "vagrant"
        PG_DB = "u_solutions_core_tests"
        PG_ENV = "-e POSTGRES_USER=${PG_USER} -e POSTGRES_PASSWORD=${PG_PASS} -e POSTGRES_DB=${PG_DB} -d"
        // Docker images
        PHP_IMAGE = "u_solutions_core_php-8.1"
        PG_IMAGE = "postgres:14"
    }

    stages {
        stage('Portainer') {
            steps {
                script {
                    def PostgresContainerID = docker.image("${PG_IMAGE}").withRun("${PG_ENV}")
                    env.PG_C_ID = PostgresContainerID
                    print "${PG_C_ID}"
                }
            }
        }
    }
    post {
        always {
            script {
                docker.stop(env.PG_C_ID)
            }
        }
    }
}
