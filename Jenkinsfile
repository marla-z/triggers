pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
        timestamps() 
    }
    environment {
        // Git
        repo = "https://github.com/marla-z/triggers.git"
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
                    pg = docker.image("${env.image_postgres}").withRun("${pg_env}")
                    mc = docker.image('memcached').withRun()
                    php = docker.image("${env.image_php}")
                }
            }
        }

        stage('Checkout') {
            steps {
                script {
                    php.inside("--link ${pg.id}:postgres --link ${mc.id}:memcached") {
                        if (env.GIT_BRANCH) {
                            branch = "${GIT_BRANCH.split('/').last()}"
                            checkout([
                                $class: 'GitSCM',
                                branches: [[name: "*/${branch}"]],
                                doGenerateSubmoduleConfigurations: false,
                                extensions: [],
                                submoduleCfg: [],
                                userRemoteConfigs: [
                                    [
                                        credentialsId: 'ACCESS_GITHUB', 
                                        url: "${repo}"
                                    ]
                                ]
                            ])
                        }
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

    post {
        always {
            script {
                pg.cleanWs()
                mc.cleanWs()
                php.cleanWs()
            }
        }
    }
}
