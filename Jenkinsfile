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
            desscreption: 'selections of yhedeplozment variables'
        )
        choice{
            name: 'dockerbvalksdb',
            choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
            desscreption: 'select the registry branch'
        }
    }
    stage{
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