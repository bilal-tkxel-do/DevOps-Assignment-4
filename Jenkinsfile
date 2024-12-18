pipeline {
    agent any  // No default agent

    environment {
	GITHUB_REPO = 'https://github.com/bilal-tkxel-do/DevOps-Assignment-4.git' // GitHub Repository URL
        CREDENTIALS_ID = 'github-token'  // Credentials ID for GitHub
        DEPLOY_ENV = 'production'
        NAME = 'Bilal'  // Set the global environment variable for your name
    }

    triggers {
        // Poll for changes or listen to webhooks
        githubPush() // Automatically triggers when a push event occurs
    }

    stages {
	stage('Clone Repository') {
            steps {
                git branch: 'main', 
                    credentialsId: "${CREDENTIALS_ID}",
                    url: "${GITHUB_REPO}"
            }
        }

        stage('Node.js Version') {
            agent {
                label 'docker'  // Assuming you have a label 'docker' for Docker-enabled agents
            }
            steps {
                script {
                    // Use Docker inside the steps block
                    docker.image('node:18').inside {
                        def nodeVersion = sh(script: 'node -v', returnStdout: true).trim()
                        echo "${nodeVersion} ${env.NAME}"
                    }
                }
            }
        }

        stage('Maven Version') {
            agent {
                label 'docker'  // Same here, 'docker' label for the Docker-enabled agent
            }
            steps {
                script {
                    // Use Docker inside the steps block
                    docker.image('maven:3.8.1-jdk-11').inside {
                        def mavenVersion = sh(script: 'mvn -v | head -n 1', returnStdout: true).trim()
                        echo "${mavenVersion} ${env.NAME}"
                    }
                }
            }
        }
    }
}

