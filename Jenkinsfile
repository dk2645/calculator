pipeline{
  agent any
    stages{
        stage('Build') {
            steps{
               
                sh 'ls'
            }
        }
        stage('Deploy') {
        environment {
            EC2_HOST = '13.126.84.247'
            EC2_USER = 'ubuntu'
            }
        steps {
                sh '''
                 rm -rf .git
                 scp -r /var/lib/jenkins/workspace/calculator_app/ ${EC2_USER}@${EC2_HOST}:/home/${EC2_USER}/
                 ssh ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/calculator_app/ && rm -rf node_modules  package-lock.json"
                 ssh ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/calculator_app/ && npm install && pm2 start app.js --name 'my node app'"
                '''
            }
        }
    }

}
