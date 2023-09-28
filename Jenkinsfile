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
                    container_pg = docker.image("${env.image_postgres}").withRun("${pg_env}")
                    container_mc = docker.image('memcached').withRun()
                    container_php = docker.image("${env.image_php}").inside("--link ${container_pg.id}:postgres --link ${container_mc.id}:memcached")
                }
            }
        }

        stage('Checkout') {
            steps {
                script {
                    container_php.inside {
                        if (env.GIT_BRANCH) {
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

        stage('Build') {
            steps {
                script {
                    println "plug"
                }
            }
        }
    }

    post {
        always {
            container_pg.cleanWs()
            container_mc.cleanWs()
            container_php.cleanWs()
        }
    }
}
