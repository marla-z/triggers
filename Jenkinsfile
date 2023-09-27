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
        def variables = currentBuild.rawBuild.properties
        variables.each { prop ->
            echo "${prop.key} = ${prop.value}"
        }

        def causes = currentBuild.rawBuild.causes
        def branchName

        causes.each { cause ->
            if (cause instanceof hudson.triggers.SCMTrigger$Cause) {
                branchName = cause.getShortDescription().split("from ")[1]
            }
        }

        echo "Branch Name: ${branchName}"
    }
}
