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
                    env.inputIp = userInput.Ip?:''
                    env.inputRepo = userInput.Repo?:''

                    // echo ("ip: ${inputIp}")
                    // echo ("repo: ${inputRepo}")
                }
            }
        }
        stage('available'){
            steps{
                script {
                    def serverAvailable = false
                    try {
                        // Try to ping the server
                        sh "ping -c 1 ${env.inputIp}"
                        serverAvailable = true
                    } catch (Exception e) {
                        echo "Server is not c: ${e.message}"
                    }

                    if (serverAvailable) {
                        echo "Server ${env.inputIp} is available."
                    } else {
                        error "Server ${env.inputIp} is not available."
                    }
                }
            }
        }
    }
}

