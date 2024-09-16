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
                
                    sh '''
                    npm install
                    cd frontend
                    npm install
                    '''
            }
        }

        stage('Build') {
            steps {
                // Build the application
                
                    sh '''
                    npm run server
                    '''
                
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
