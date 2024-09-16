pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/m-adilazan/mern-tutorial.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Ensure the environment has Node.js
                dir("mern-tutorial") {
                    sh '''
                    npm install
                    '''
                }
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests
                dir("mern-tutorial") {
                    sh '''
                    npm test
                    '''
                }
            }
        }

        stage('Build') {
            steps {
                // Build the application
                dir("mern-tutorial") {
                    sh '''
                    npm run build
                    '''
                }
            }
        }

        stage('Deploy to Remote Server') {
            steps {
                sshagent(['server-credentials']) {
                    sh '''
                    scp -r * VMSYS@98.70.11.5:/home/VMSYS
                    ssh VMSYS@98.70.11.5 "cd /home/VMSYS && npm install && pm2 restart all"
                    '''
                }
            }
        }
    }
}
