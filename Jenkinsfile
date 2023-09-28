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
                    def postgresId = docker.image("${PG_IMAGE}").withRun("${PG_ENV} -d")
                    def memcachedId = docker.image('memcached').withRun('-d')
                    def phpId = docker.image("${PHP_IMAGE}").withRun("-d --link ${postgresId}:postgres --link ${memcachedId}:memcached")
                    
                    env.PHP_CONTAINER_ID = phpId
                }
            }
        }

        stage('Checkout') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Checkout"
                    }
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Build"
                    }
                }
            }
        }

        stage('Sniffer') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Sniffer"
                    }
                }
            }
        }
        
        stage('Psalm') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Psalm"
                    }
                }
            }
        }

        stage('Codeception') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Codeception"
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def phpContainerId = env.PHP_CONTAINER_ID
                    docker.image("${IMAGE_PHP}").inside("--volumes-from ${phpContainerId}") {
                        print "Deploy"
                    }
                }
            }
        }                    
    }

    post {
        always {
            script {
                docker.stop(env.PHP_CONTAINER_ID)
                docker.stop(env.PG_CONTAINER_ID)
                docker.stop(env.MC_CONTAINER_ID)
            }
        }
    }
}
