pipeline {
    agent { label 'runner' }
    stages {
        stage('Get All Environment Variables') {
            steps {
                script {
                    sh 'env'
                }
            }
        }
    }
}
