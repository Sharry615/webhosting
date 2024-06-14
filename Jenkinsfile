pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the version control system (e.g., Git)
                git 'https://github.com/your-repo/webhosting.git'
            }
        }

        stage('Build') {
            steps {
                // Since this is a static HTML project, there is no build step
                echo 'No build step needed for HTML project'
            }
        }

        stage('Test') {
            steps {
                // Run some basic tests to ensure the HTML is valid
                echo 'Running HTML validation tests...'
                sh '''
                # Example: Use a tool like tidy to validate HTML
                # Install tidy if not already installed
                sudo apt-get install -y tidy
                # Validate all HTML files
                find . -name "*.html" -exec tidy -errors {} \;
                '''
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the HTML files to a web server or a static hosting service
                echo 'Deploying HTML files...'
                sh '''
                # Example: Copy files to /var/www/html (assuming a local web server setup)
                sudo cp -r * /var/www/html/
                '''
            }
        }
    }

    post {
        always {
            // Clean up workspace
            cleanWs()
        }
        success {
            // Notify success
            echo 'Build, test, and deployment successful'
        }
        failure {
            // Notify failure
            echo 'Build, test, or deployment failed'
        }
    }
}
