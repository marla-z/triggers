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
        // Docker images
        PHP_IMAGE = "u_solutions_core_php-8.1"
        PG_IMAGE = "postgres:14"
    }

    stages {
        stage('Portainer') {
            steps {
                script {
                    def postgresId = sh(script: "docker run -d ${PG_IMAGE} -e POSTGRES_USER=${PG_USER} -e POSTGRES_PASSWORD=${PG_PASS} -e POSTGRES_DB=${PG_DB}", returnStdout: true).trim()
                    def memcachedId = sh(script: 'docker run -d memcached', returnStdout: true).trim()
                    def phpId = sh(script: "docker run -d --link ${postgresId}:postgres --link ${memcachedId}:memcached ${PG_IMAGE}", returnStdout: true).trim()
                    // Passing the containers ID to the next steps
                    env.PHP_CONTAINER_ID = phpId
                    env.PG_CONTAINER_ID = postgresId
                    env.MC_CONTAINER_ID = memcachedId
                }
            }
        }

        stage('Print') {
            println "\
                \nphp             ${PHP_CONTAINER_ID}\
                \npg              ${PG_CONTAINER_ID}\
                \nmc              ${MC_CONTAINER_ID}\
            "
        }
    }

    post {
        always {
            script {
                sh "docker stop ${env.PHP_CONTAINER_ID}"
                sh "docker stop ${env.PG_CONTAINER_ID}"
                sh "docker stop ${env.MC_CONTAINER_ID}"
                sh "docker rm ${env.PHP_CONTAINER_ID}"
                sh "docker rm ${env.PG_CONTAINER_ID}"
                sh "docker rm ${env.MC_CONTAINER_ID}"
            }
        }
    }
}
