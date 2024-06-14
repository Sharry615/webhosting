pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Sharry615/webhosting.git'
        BRANCH = 'main'
        DEPLOY_DIR = '/var/www/html/webhosting'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out the code...'
                // Clean workspace before checkout
                deleteDir()
                // Checkout the repository
                git branch: "${env.BRANCH}", url: "${env.REPO_URL}"
            }
        }

        stage('Clean Previous Deployment') {
            steps {
                echo 'Cleaning previous deployment...'
                // Remove previous data
                sh "rm -rf ${env.DEPLOY_DIR}/*"
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Commands to build the project
                // For example, if it's a Node.js project:
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Commands to run tests
                // For example, if it's a Node.js project:
                sh 'npm test'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying the new build...'
                // Copy new data to the deployment directory
                sh "cp -r * ${env.DEPLOY_DIR}/"
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            // Clean up workspace
            deleteDir()
        }
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed!'
        }
    }
}
