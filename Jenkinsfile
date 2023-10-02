pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    def branchName = env.GIT_BRANCH
                    println "істанній коміт був в гілку: ${branchName}"
                }
            }
        }
    }
}
