node('runner') {
    checkout([
        $class: 'GitSCM',
        branches: [[name: "main"]],
        doGenerateSubmoduleConfigurations: false,
        extensions: [],
        submoduleCfg: [],
        userRemoteConfigs: [[
            credentialsId: 'ACCESS_GITHUB',
            url: 'https://github.com/marla-z/triggers.git'
        ]]
    ])
    stage("Env") {
        echo 'hello from common section'
        echo "BRANCH_NAME: ${env.GIT_BRANCH.split("/")[1]}"
    }
}
