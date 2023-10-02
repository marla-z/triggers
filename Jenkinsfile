pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    // Вивести всі змінні середовища
                    env.each { k, v ->
                        echo "${k}=${v}"
                    }
                }
            }
        }
    }
}
