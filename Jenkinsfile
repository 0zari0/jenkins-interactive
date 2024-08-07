pipeline{
    agent any
    environment {
        GIT_SSH_KEY = credentials('jenkins-private-key')  
        DOCKER_CREDENTIALS_ID = 'iakos-registry' 
        DOCKER_REGISTRY_URL = 'https://172.20.0.36:5000'  
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
        stage('server available'){
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
        stage('List Docker Repositories') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                        // Make an HTTP GET request to the Docker Registry API to list repositories
                        try {
                            def response = httpRequest url: "${DOCKER_REGISTRY_URL}/v2/_catalog", httpMode: 'GET', contentType: 'APPLICATION_JSON',
                                                       authentication: "${DOCKER_CREDENTIALS_ID}"

                            // Log the entire response
                            echo "HTTP Response: ${response}"

                            // Parse the JSON response
                            def jsonResponse = readJSON text: response.content

                            // Print out the list of repositories
                            def repositories = jsonResponse.repositories
                            echo "Docker Repositories:"
                            for (repo in repositories) {
                                echo "- ${repo}"
                            }
                        } catch (Exception e) {
                            echo "Error during HTTP request: ${e}"
                        }
                    }
                }
            }
        }
    }
}

