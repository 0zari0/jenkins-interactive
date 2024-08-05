pipeline{
    agent {
        label 'jenkins-agent'
    }
    environment{
        GIT_SSH_KEY = credentials('jenkins-private-key')
        DOCKER_CREDENTIALS_ID = 'iakos-registry'
        DOCKER_REGISTRY = '172.20.0.36:5000'
    }
    parameters{
        choice(
            name: 'server-ip',
            choices: ['172.20.5.6','172.20.5.5'],
            description: 'selections of yhedeplozment variables'
        )
        // choice{
        //     name: 'dockerbvalksdb',
        //     choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
        //     description: 'select the registry branch'
        // }
    }
    stages{
        stage('Get informations of repo') {
            steps {
                script {
                    echo "Start of the build"
                    try {
                        scmVars = checkout scm
                        echo "Gathering checksums"
                        echo "Stage Init after checkout scm"
                        
                        branch = utils.branchName(scmVars)
                        env.BRANCH = branch
                        pomVersion = readMavenPom(file: 'pom.xml').version
                        commitId = utils.shortCommitId(scmVars.GIT_COMMIT)
                        time = new Date().format('yyMMddHHmm')
                        //get repo name
                        def scmUrl = scmVars.GIT_URL
                        def repoName = scmUrl.tokenize('/').last().replace('.git', '')
                        env.REPO_NAME = repoName

                        //get tag 
                        def tag
                        try {
                            tag = sh(script: 'git describe --tags `git rev-list --tags --max-count=1` || echo "none"', returnStdout: true).trim()
                        } catch (Exception e) {
                            echo "No tags found or an error occurred: ${e}"
                            tag = "none"
                        }
                        env.COMMIT_ID = commitId
                        env.TAG = tag
                        env.TIME = time
                        echo "Repo: ${env.REPO_NAME}"
                        echo "Branch: ${env.BRANCH}"
                        echo "Tag: ${env.TAG}"                        
                        echo "Commit ID: ${env.COMMIT_ID}"
                        echo "Time: ${env.TIME}"

                    } catch (Exception e) {
                            echo "Error during checkout stage: ${e}"
                            throw e
                    }
                }
            }
        }
        stage('Interactive deployment'){
            steps{
                script{
                    echo "the selected is  ${params.server-ip}"

                }
            }
        }
    }
}