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
        stage('Checkout') {
            steps {
                script {
                    echo "Start of the build"
                    try {
                        def scmVars = checkout([
                            $class: 'GitSCM',
                            branches: [[name: '*/main']],
                            doGenerateSubmoduleConfigurations: false,
                            extensions: [[$class: 'CleanBeforeCheckout']],
                            userRemoteConfigs: [[
                                url: 'git@github.com:0zari0/jenkins-interactive.git',
                                credentialsId: 'GIT_SSH_KEY'
                            ]]
                        ])
                        echo "Checked out successfully."
                        echo "Repository URL: ${scmVars.GIT_URL}"
                        echo "Repository Branch: ${scmVars.GIT_BRANCH}"
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