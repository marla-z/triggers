pipeline {
    agent any
    stages {
        stage('Example') {
            steps {
                script {
                    def branchName = env.BRANCH_NAME
                    echo "Останній коміт був в гілку: ${branchName}"
                    echo "print"
                }
            }
        }
    }
}
