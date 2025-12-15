pipeline {
    agent any

    environment {
        DEPLOY_USER = 'azureuser'
        DEPLOY_HOST = '40.81.29.181'
        SSH_KEY_ID = 'azure-vm-key'
        APP_DIR = '/home/azureuser/my-website'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/UzairHassan409/jenkins_project.git'
            }
        }

        stage('Deploy to Azure VM') {
            steps {
                sshagent([SSH_KEY_ID]) {
                    sh """
                    ssh -o StrictHostKeyChecking=no $DEPLOY_USER@$DEPLOY_HOST "mkdir -p $APP_DIR"
                    scp -o StrictHostKeyChecking=no -r * $DEPLOY_USER@$DEPLOY_HOST:$APP_DIR/
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
