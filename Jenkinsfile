pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    def branchName = env.GIT_BRANCH
                    println "Останній коміт був в гілку: ${branchName}"
                }
            }
        }
    }
}
