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
        // Docker
        PHP_IMAGE = "u_solutions_core_php-8.1"
        PG_IMAGE = "postgres:14"
        MC_IMAGE = "memcached"
    }

    stages {
        stage('Portainer') {
            steps {
                script {
                    // Setup postgresql container
                    def PostgresContainerID = sh(script: "docker run -d ${PG_IMAGE} ${PG_ENV}", returnStdout: true).trim()
                    env.PG_C_ID = PostgresContainerID
                    // Setup memcached container
                    def MemcachedContainerID = sh(script: "docker run -d ${MC_IMAGE}", returnStdout: true).trim()
                    env.MC_C_ID = MemcachedContainerID
                    // Setup php container
                    def PhpContainerID = sh(script: "docker run -d ${PHP_IMAGE} --link ${PG_C_ID}:postgres --link ${MC_C_ID}:memcached", returnStdout: true).trim()
                    env.PHP_C_ID = PhpContainerID
                }
            }
        }
    }
    post {
        always {
            script {
                sh "docker stop ${PG_C_ID} ${MC_C_ID} ${PHP_C_ID}"
                sh "docker rm ${PG_C_ID} ${MC_C_ID} ${PHP_C_ID}"
            }
        }
    }
}
