pipeline {
    agent any

    environment {
        PATH = "/var/jenkins_home/.local/state/fnm_multishells/3385_1726483073533/bin/:$PATH"  // Use the path obtained from `which node` and `which npm`
    }
    
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
                    cd frontend
                    npm run build
                    '''
                
            }
        }

        stage('Deploy to Remote Server') {
            steps {
                sshagent(['adm-m-adilazan@4.247.131.4']) {
                    sh '''
                    scp -r * VMSYS@98.70.11.5:/home/VMSYS
                    ssh VMSYS@98.70.11.5 "cd /home/VMSYS && npm install && pm2 restart all"
                    '''
                }
            }
        }
    }
}
