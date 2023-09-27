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
        params.each {param ->
            println "${param.key} -> ${param.value} "
        }
    }
    echo "GWBT_COMMIT_BEFORE:  $GWBT_COMMIT_BEFORE"
    echo "GWBT_COMMIT_AFTER:   $GWBT_COMMIT_AFTER"
    echo "GWBT_REF:            $GWBT_REF"
    echo "GWBT_TAG:            $GWBT_TAG"
    echo "GWBT_BRANCH:         $GWBT_BRANCH"
    echo "GWBT_REPO_CLONE_URL: $GWBT_REPO_CLONE_URL"
    echo "GWBT_REPO_HTML_URL:  $GWBT_REPO_HTML_URL"
    echo "GWBT_REPO_FULL_NAME: $GWBT_REPO_FULL_NAME"
    echo "GWBT_REPO_NAME:      $GWBT_REPO_NAME"
}
