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
        PG_ENV = "-e POSTGRES_USER=${PG_USER} -e POSTGRES_PASSWORD=${PG_PASS} -e POSTGRES_DB=${PG_DB}"
        // Docker images
        PHP_IMAGE = "u_solutions_core_php-8.1"
        PG_IMAGE = "postgres:14"
    }

    stages {
        stage('Portainer') {
            steps {
                script {
                    docker.image("${PG_IMAGE}").withRun("${PG_ENV}") { c ->
                        docker.image('memcached').withRun() { mk ->
                            docker.image("${PHP_IMAGE}").inside("--link ${c.id}:postgres --link ${mk.id}:memcached") {
                                echo "Print"
                            }
                        }
                    }
                }
            }
        }
    }
}
