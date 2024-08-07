pipeline {
    agent none
    environment {
        GIT_SSH_KEY = credentials('jenkins-private-key')
        DOCKER_CREDENTIALS_ID = 'iakos-registry'
        DOCKER_REGISTRY = '172.20.0.36:5000'
    }
    stages {
        stage('Interactive deployment') {
            agent {
                label 'jenkins-agent'
            }
            steps {
                script {
                    // Use a node block to ensure the necessary context
                    node('jenkins-agent') {
                        withCredentials([sshUserPrivateKey(credentialsId: 'jenkins-private-key', keyFileVariable: 'GIT_SSH_KEY')]) {
                            def userInput = input(id: 'userInput', message: 'Provide your inputs', parameters: [
                                string(defaultValue: 'Dave', description: 'What is your first name?', name: 'FIRST_NAME', trim: true),
                                choice(name: 'doker_Repository', choices: ['jenkins2.0-hotfix', 'jenkins2.0-main'], description: 'Selection of the repository')
                            ])
                            
                            echo "The selected test environment is ${userInput.FIRST_NAME}"
                            echo "The selected repository is ${userInput.doker_Repository}"
                        }
                    }
                }
            }
        }
    }
}

