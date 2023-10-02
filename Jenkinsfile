pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    def branchName = env.GIT_BRANCH
                    echo "Останній коміт був в гілку: ${branchName}"
                }
            }
        }
    }
}
