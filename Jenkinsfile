pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Pull the code from your repository
                git branch: 'main', url: 'https://github.com/m-adilazan/mern-tutorial.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install npm dependencies
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Build the application (if needed)
                sh 'npm run build'
            }
        }

        stage('Deploy to Remote Server') {
            steps {
                // SCP or SSH deployment
                // For Dockerized applications, use Docker commands to deploy
                sshagent(['server-credentials']) {
                    sh 'scp -r * VMSYS@98.70.11.5:/home/VMSYS'
                    sh 'ssh VMSYS@98.70.11.5 "cd /home/VMSYS && npm install && pm2 restart all"'
                }
            }
        }
    }
}
