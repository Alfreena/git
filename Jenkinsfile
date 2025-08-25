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
                // sshagent(['my-ssh-key']) {
                //     sh '''
                //     ssh user@your-server-ip "
                //         cd /var/www/myapp &&
                //         git pull origin main &&
                //         docker-compose down &&
                //         docker-compose up -d --build
                //     "
                //     '''
                echo "Starting application locally..."
                sh 'nohup python app.py > app.log 2>&1 &'
            }
        }
    }
}
