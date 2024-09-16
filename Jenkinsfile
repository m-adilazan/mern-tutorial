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
                    /var/jenkins_home/workspace/Node JS Pipeline/mern-tutorial/npm install
                    '''
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests
                
                    sh '''
                    /var/jenkins_home/workspace/Node JS Pipeline/mern-tutorial/npm test
                    '''
                
            }
        }

        stage('Build') {
            steps {
                // Build the application
                
                    sh '''
                    /var/jenkins_home/workspace/Node JS Pipeline/mern-tutorial/npm run build
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
