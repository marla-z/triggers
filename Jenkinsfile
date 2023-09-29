pipeline {
    agent any

    environment {
        CHANGE_BRANCH = sh(script: 'git rev-parse --abbrev-ref HEAD', returnStdout: true).trim()
    }

    stages {
        stage('Отримання коду з SCM') {
            steps {
                script {
                    checkout scm
                }
            }
        }
    }

    post {
        always {
            script {
                if (env.CHANGE_BRANCH) {
                    echo "Пайплайн був запущений з гілки ${env.CHANGE_BRANCH}"
                } else {
                    echo 'Пайплайн був запущений вручну'
                }
            }
        }
    }
}
