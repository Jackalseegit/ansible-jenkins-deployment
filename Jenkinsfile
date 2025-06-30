pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/your-username/ansible-jenkins-deployment.git'
            }
        }

        stage('Run Ansible') {
            steps {
                sshagent(['e3af536f-7ac5-40c5-8f98-12572dcd4bba']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ec2-user@172.31.82.65 '
                      cd ansible-jenkins-deployment &&
                      ansible-playbook -i inventory/production site.yml
                    '
                    '''
                }
            }
        }
    }
}
