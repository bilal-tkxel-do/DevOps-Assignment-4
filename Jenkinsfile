pipeline {
    agent any
    environment {
        GITHUB_REPO = 'https://github.com/bilal-tkxel-do/DevOps-Assignment-4.git' // GitHub Repository URL
        CREDENTIALS_ID = 'github-token'  // Credentials ID for GitHub
        DEPLOY_ENV = 'production'       // Deployment environment
        NAME = 'Bilal'                 // Your name
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
        stage('Build') {
            agent {
                docker { image 'node:14' } // Node.js build environment
            }
            steps {
                sh 'node -v'
                echo "Node.js build completed by ${NAME}"
            }
        }        
	stage('Node.js Version') {
            agent {
                label 'docker'  
            }
            steps {
                script {
                    docker.image('node:18').inside {
                        def nodeVersion = sh(script: 'node -v', returnStdout: true).trim()
                        echo "${nodeVersion} ${env.NAME}"
                    }
                }
            }
        }

        stage('Maven Version') {
            agent {
                label 'docker'  
            }
            steps {
                script {
                        docker.image('maven:3.8.1-jdk-11').inside {
                        def mavenVersion = sh(script: 'mvn -v | head -n 1', returnStdout: true).trim()
                        echo "${mavenVersion} ${env.NAME}"
                    }
                }
            }
        }
    }
}

