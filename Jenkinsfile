pipeline {
    agent any
    environment {
        GITHUB_REPO = 'https://github.com/bilal-tkxel-do/DevOps-Assignment-4.git' 
        CREDENTIALS_ID = 'github-token'  
        DEPLOY_ENV = 'production'       
        NAME = 'Bilal'                 
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

