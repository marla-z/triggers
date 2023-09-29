pipeline {
    agent { label "runner" }
 
    stages {
        stage('Перевірка Jenkinsfile') {
            steps {
                script {
<<<<<<< HEAD
                    sh "env"
=======
                    // Setup postgresql container
                    def PostgresContainerID = sh(script: "docker run -d ${PG_IMAGE} ${PG_ENV}", returnStdout: true).trim()
                    env.PG_C_ID = PostgresContainerID
                    // Setup memcached container
                    def MemcachedContainerID = sh(script: "docker run -d ${MC_IMAGE}", returnStdout: true).trim()
                    env.MC_C_ID = MemcachedContainerID
                    // Setup php container
                    def PhpContainerID = sh(script: "docker run -d ${PHP_IMAGE} --link ${PG_C_ID}:postgres --link ${MC_C_ID}:memcached", returnStdout: true).trim()
                    env.PHP_C_ID = PhpContainerID

                    println "Containers:\
                        \n    Postgresql      --      ${PG_C_ID}\
                        \n    Memcached       --      ${MC_C_ID}\
                        \n    Php             --      ${PHP_C_ID}\
                    "

                    println "Git params:\
                        \n    Selected branch --      ${Branch}\
                        \n    Branch:         --      ${GIT_BRANCH}\
                        \n    Repository      --      ${REPO}\
                    "
                    if (currentBuild.causes.toString().contains('UserIdCause')) {
                        println 'Цей пайплайн був запущений вручну'
                    } else {
                        println 'Цей пайплайн був запущений автоматично'
                    }
>>>>>>> main
                }
            }
        }

        // Додай інші етапи тут
    }
}
