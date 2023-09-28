pipeline {
    agent { label 'runner' }
    options {
        ansiColor('xterm')
        timestamps() 
    }
    environment {
        // Git
        branch = "${env.Branch.split('/').last()}"
        repo = "https://github.com/marla-z/triggers.git"
        // Postgres
        pg_user = "vagrant"
        pg_pass = "vagrant"
        pg_db = "u_solutions_core_tests"
        pg_env = "-e POSTGRES_USER=${pg_user} -e POSTGRES_PASSWORD=${pg_pass} -e POSTGRES_DB=${pg_db}"
    }
    stages {
        stage('Init') {
            steps {
                script {
                    c_pg = docker.image("${env.image_postgres}").withRun("${pg_env}")
                    c_mc = docker.image('memcached').withRun()
                    c_php = docker.image("${env.image_php}").inside("--link ${c_pg.id}:postgres --link ${c_mc.id}:memcached")
                }
            }
        }

        stage('Checkout') {
            steps {
                script {
                    php.inside {
                        if (env.GIT_BRANCH}) {
                            // Trigger git hook
                            branch = "${GIT_BRANCH.split('/').last()}"
                        }
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

        stage('Stage 2') {
            steps {
                script {
                }
            }
        }
    }

    post {
        always {
            // Закрити всі контейнери після завершення пайплайну
            c_pg.cleanWs()
            c_mc.cleanWs()
            c_php.cleanWs()
        }
    }
}
