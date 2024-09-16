pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/m-adilazan/mern-tutorial.git'
            }
        }

        stage('Install Node.js using fnm') {
            steps {
                // Install fnm and Node.js 20 using fnm
                sh '''
                curl -fsSL https://fnm.vercel.app/install | bash
                source ~/.bashrc || true
                fnm use --install-if-missing 20

                # Verify Node.js and npm versions
                node -v
                npm -v
                '''
            }
        }

        stage('Install Dependencies') {
            steps {
                // Ensure the environment has Node.js
                sh '''
                source ~/.bashrc || true
                npm install
                '''
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests
                sh '''
                source ~/.bashrc || true
                npm test
                '''
            }
        }

        stage('Build') {
            steps {
                // Build the application
                sh '''
                source ~/.bashrc || true
                npm run build
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
