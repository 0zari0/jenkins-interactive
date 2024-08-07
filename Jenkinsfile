pipeline{
    agent none
    environment{
        GIT_SSH_KEY = credentials('jenkins-private-key')
        DOCKER_CREDENTIALS_ID = 'iakos-registry'
        DOCKER_REGISTRY = '172.20.0.36:5000'
    }
    parameters{
        input{
            message "What is your first name?".
            ok "Submit".
            defaultValue: 'Dave',
            name: 'FIRST_NAME',
            trim: true
        }
        choice{
            name: 'doker_Repository',
            choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
            description: 'selection of the repository'
        }
    }
    stages{
        stage('Interactive deployment'){
            steps{
                script{
                    echo "the selected test envirament is  ${params.FIRST_NAME}"
                    echo "the selected repository is ${params.doker_Repository}"
                }
            }
        }
    }
}