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
                sshagent(['9fc950f1-b26c-45a3-8198-ab80799c59d8']) {
                    sh '''
                    mkdir -p ~/.ssh
                    echo "Host *" >> ~/.ssh/config
                    echo "    StrictHostKeyChecking no" >> ~/.ssh/config
                    chmod 600 ~/.ssh/config
                    scp -r * VMSYS@98.70.11.5:/home/VMSYS
                    ssh VMSYS@98.70.11.5 "cd /home/VMSYS && npm install && sudo npm install -g pm2 && pm2 restart all"
                    '''
                }
            }
        }
    }
}
