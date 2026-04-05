pipeline {
    agent any
    parameters {
        gitParameter defaultValue: 'master',
                     description: 'Branch of git parameter plugin',
                     name: 'GIT_PARAMETER_PLUGIN_BRANCH',
                     type: 'GitParameterDefinition',
                     useRepository: 'git@github.com:jenkinsci/git-parameter-plugin.git'
        gitParameter defaultValue: 'master',
                     description: 'Branch of git client plugin',
                     name: 'GIT_CLIENT_PLUGIN_BRANCH',
                     type: 'GitParameterDefinition',
                     useRepository: 'git@github.com:jenkinsci/git-client-plugin.git'
    }
    stages {
        stage('checkout-2-repos') {
            steps {
                dir('git-parameter-plugin') {
                    checkout scmGit(branches: [[name: params.GIT_PARAMETER_PLUGIN_BRANCH]],
                                    extensions: [cloneOption(depth: 1, honorRefspec: true, noTags: true, shallow: true),
                                                 localBranch()],
                                    userRemoteConfigs: [[credentialsId: 'github-ed25519',
                                                         url: 'git@github.com:jenkinsci/git-parameter-plugin.git']])
                    sh 'git branch; git log -n 1; head README*'
                }
                dir('git-client-plugin') {
                    checkout scmGit(branches: [[name: params.GIT_CLIENT_PLUGIN_BRANCH]],
                                    extensions: [cloneOption(depth: 1, honorRefspec: true, noTags: true, shallow: true),
                                                 localBranch()],
                                    userRemoteConfigs: [[credentialsId: 'github-ed25519',
                                                         url: 'git@github.com:jenkinsci/git-client-plugin.git']])
                    sh 'git branch; git log -n 1; head README*'
                }
            }
        }
    }
}
