pipeline{
    agent {
        label 'jenkins-agent'
    }
    environment{
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
        stage('Interactive deployment'){
            steps{
                script{
                    def inputIp
                    def inputTAg

                    echo "the selected avbsa ${params.server-ip}"

                }
            }
        }
    }
}