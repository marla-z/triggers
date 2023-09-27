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
        def causes = currentBuild.rawBuild.getCauses()

        def branchName = null

        causes.each { cause ->
            if (cause.class.toString() == 'class hudson.triggers.SCMTrigger$Cause') {
                branchName = cause.shortDescription.split('from ')[1]
            }
        }   
        echo "Branch Name: ${branchName}"
    }
}
