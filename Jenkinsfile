pipeline {
    agent any
    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }
    tools {
        ansible 'ansible' // if defined in Jenkins global tool config
    }
    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Jackalseegit/ansible-jenkins-deployment.git',
                    branch: 'main',
                    credentialsId: 'github-creds' // make sure this ID exists
            }
        }
        stage('Run Ansible') {
            steps {
                sh '''
                ansible-playbook -i inventory/production site.yml
                '''
            }
        }
    }
}
