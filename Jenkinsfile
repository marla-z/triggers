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
        def envVars = currentBuild.rawBuild.envVars

        envVars.each { key, value ->
            println "Environment Variable: ${key} = ${value}"
        }
    }
}
