stage('Build') {
            steps {
                sh 'npm install'
                sh 'pwd'
                sh 'ls'
            }
        }
stage('Deploy') {
    environment {
        SSH_KEY = credentials('')
        EC2_HOST = ''
        EC2_USER = 'ubuntu'
        }
    steps {
            withCredentials([sshUserPrivateKey(credentialsId: '', keyFileVariable: 'SSH_KEY')]) {
            sh '''
            pwd
            ls
            scp -o "StrictHostKeyChecking=no" -r ./dist ${EC2_USER}@${EC2_HOST}:/home/${EC2_USER}/
            ssh -o "StrictHostKeyChecking=no" -i ${SSH_KEY} ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/app && npm install && pm2 start app.js --name "my app""
            '''
            }
        }
}
