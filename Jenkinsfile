pipeline {
    agent any
    stages {
        stage('Get All Environment Variables') {
            steps {
                script {
                    sh "env"
                    
                    sh "echo ${GIT_BRANCH}"
                }
            }
        }
    }
}
