pipeline{
    agent any
    environment {
        GIT_SSH_KEY = credentials('jenkins-private-key')  
        DOCKER_CREDENTIALS_ID = 'iakos-registry' 
        DOCKER_REGISTRY_URL = 'https://172.20.0.36:5000' 
        DOCKER_USERNAME = 'azarandok'
        DOCKER_PASSWORD = 'wf81nh17roro'
    }
    stages{        
        stage('Fetch Docker Repositories') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
                        // Fetch the list of repositories
                        def response = sh(script: "curl -k -u ${DOCKER_USERNAME}:${DOCKER_PASSWORD} ${DOCKER_REGISTRY_URL}/v2/_catalog", returnStdout: true).trim()

                        // Parse the JSON response
                        def jsonResponse = readJSON text: response

                        // Extract the repository names
                        def repositories = jsonResponse.repositories
                        echo "Docker Repositories:"
                        for (repo in repositories) {
                            echo "- ${repo}"
                        }

                        // Convert the list of repositories to a string that can be used in the next step
                        env.REPO_CHOICES = repositories.join(',')
                    }
                }
            }
        }           
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
                                value: "${env.REPO_CHOICES}",
                                // choices: ['jenkins2.0-hotfix','jenkins2.0-main'],
                                description: 'Select a Docker repository',

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
        // stage('List Docker Repositories') {
        //     steps {
        //         script {
        //             // Run the curl command to get the list of Docker repositories
        //             def response = sh(script: "curl -k -u ${DOCKER_USERNAME}:${DOCKER_PASSWORD} ${DOCKER_REGISTRY_URL}/v2/_catalog", returnStdout: true).trim()

        //             // Parse the JSON response
        //             def jsonResponse = readJSON text: response

        //             // Print out the list of repositories
        //             def repositories = jsonResponse.repositories
        //             echo "Docker Repositories:"
        //             for (repo in repositories) {
        //                 echo "- ${repo}"
        //             }
        //         }
        //     }
        // }
    }
}

