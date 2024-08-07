pipeline{
    agent any
    environment {
        GIT_SSH_KEY = credentials('jenkins-private-key')  
        DOCKER_CREDENTIALS_ID = 'iakos-registry' 
        DOCKER_REGISTRY = '172.20.0.36:5000'  
    }
    stages{
        stage("input"){
            steps{
                script{
                    def inputIp
                    def inputRepo

                    def userInput = input(
                        id: 'userInput', message: 'Plese fill out:?',
                        parameters: [
                            string(defaultValue: 'pl: 172.20.5.5',
                                    description: 'ip of the server',
                                    trim: true,
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

