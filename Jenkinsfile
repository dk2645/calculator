stage('Deploy') {
            environment {
                EC2_HOST = 'your-ec2-instance-ip'
                EC2_USER = 'ec2-user'
                EC2_PASSWORD = 'your-ec2-user-password'
            }
            steps {
                sh '''
                    sshpass -p ${EC2_PASSWORD} scp -o "StrictHostKeyChecking=no" -r ./dist ${EC2_USER}@${EC2_HOST}:/home/${EC2_USER}/app
                    sshpass -p ${EC2_PASSWORD} ssh -o "StrictHostKeyChecking=no" ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/app && npm install && pm2 startOrReload ecosystem.config.js --env production"
                '''
            }
        }
stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy') {
            environment {
                SSH_KEY = credentials('ec2-ssh-key')
                EC2_HOST = 'ec2-instance--ip'
                EC2_USER = 'ec2-user'
            }
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: 'ec2-ssh-key', keyFileVariable: 'SSH_KEY')]) {
                    sh '''
                        scp -o "StrictHostKeyChecking=no" -r ./dist ${EC2_USER}@${EC2_HOST}:/home/${EC2_USER}/app
                        ssh -o "StrictHostKeyChecking=no" -i ${SSH_KEY} ${EC2_USER}@${EC2_HOST} "cd /home/${EC2_USER}/app && npm install && pm2 startOrReload ecosystem.config.js --env production"
                    '''
                }
            }
        }

