pipeline {
    agent any
    parameters {
        gitParameter defaultValue: 'master', description: 'Branch of git plugin for checkout', name: 'GIT_PLUGIN_BRANCH', type: 'GitParameterDefinition', useRepository: 'https://github.com/jenkinsci/git-plugin.git'
        gitParameter defaultValue: 'master', description: 'Branch of git client plugin for checkout', name: 'GIT_CLIENT_PLUGIN_BRANCH', type: 'GitParameterDefinition', useRepository: 'https://github.com/jenkinsci/git-client-plugin.git'
    }
    stages {
        stage('checkout-2-repos') {
            steps {
                dir('git-plugin') {
                    checkout scmGit(branches: [[name: params.GIT_PLUGIN_BRANCH]], 
                                    extensions: [cloneOption(depth: 1, honorRefspec: true, noTags: true, shallow: true),
                                                 localBranch()], 
                                    userRemoteConfigs: [[url: 'https://github.com/jenkinsci/git-plugin.git']])
                }
                dir('git-client-plugin') {
                    checkout scmGit(branches: [[name: params.GIT_CLIENT_PLUGIN_BRANCH]], 
                                    extensions: [cloneOption(depth: 1, honorRefspec: true, noTags: true, shallow: true),
                                                 localBranch()], 
                                    userRemoteConfigs: [[url: 'https://github.com/jenkinsci/git-client-plugin.git']])
                }
                sh '(cd git-plugin && git branch && git log -n 1); (cd git-client-plugin && git branch && git log -n 1)'
            }
        }
    }
}
