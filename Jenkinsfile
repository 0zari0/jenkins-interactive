Pipeline{
    agent any
    environment {
        GIT_SSH_KEY = credentials('jenkins-private-key')  
        DOCKER_CREDENTIALS_ID = 'iakos-registry' 
        DOCKER_REGISTRY = '172.20.0.36:5000'  
    }
    stages{
        stage("asking"){
            steps{
                script{
                    def inputIp
                    def inputRepo

                    def userInput = input(
                        id: 'userInput', message: 'adj meg valamit:?',
                        parameters: [
                            string(defaultValue: 'INT',
                                    description: 'ip of the server',
                                    name: 'Ip'),
                            choice(
                                name: 'Repo',
                                choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
                                description: 'selection of the repository')

                        ]
                    )
                    inputIp = userInput.Ip?:''
                    inputRepo = userInput.Repo?:''

                    echo ("ip: ${inputIp}")
                    echo ("repo: ${inputRepo}")

                }
            }
        }
    }
}

