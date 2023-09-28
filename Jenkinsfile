pipeline {
    agent any
    stages {
        stage('Get All Environment Variables') {
            steps {
                script {
                    env.keySet().each { key ->
                        echo "${key}: ${env[key]}"
                    }
                }
            }
        }
    }
}
