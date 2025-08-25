pipeline {
    agent any
    triggers {
        githubPush()  
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Alfreena/git.git'
            }
        }
        stage('Build') {
            steps {
                sh 'echo "Building application..."'
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "Running tests..."'
                sh 'pytest'
            }
        }
        stage('Deploy') {
            steps {
                sshagent(['your-ssh-credential-id']) {
                    sh '''
                    ssh user@your-server-ip "
                        cd /var/www/myapp &&
                        git pull origin main &&
                        docker-compose down &&
                        docker-compose up -d --build
                    "
                    '''
                }
            }
        }
    }
}
