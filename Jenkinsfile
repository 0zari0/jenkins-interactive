pipeline{
    agent none
    environment{
        GIT_SSH_KEY = credentials('jenkins-private-key')
        DOCKER_CREDENTIALS_ID = 'iakos-registry'
        DOCKER_REGISTRY = '172.20.0.36:5000'
    }
    // parameters{
    //     choice(
    //         name: 'test_Environment',
    //         choices: ['INT','KTN','HUN'],
    //         description: 'selections of test enviroment options'
    //     )
    //     choice{
    //         name: 'doker_Repository',
    //         choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
    //         description: 'selection of the repository'
    //     }
    // }
    stages{
        stage('Interactive deployment'){
            steps{
                script{
                    echo "the selected test envirament is  ${params.test_Environment}"
                    echo "the selected repository is ${params.doker_Repository}"
                }
            }
        }
    }
}