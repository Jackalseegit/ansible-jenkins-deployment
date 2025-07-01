pipeline {
  agent any

  stages {
    stage('Checkout Git') {
      steps {
        git branch: 'main',
            credentialsId: 'your-git-creds-id',
            url: 'https://github.com/Jackalseegit/ansible-jenkins-deployment.git'
      }
    }

    stage('Copy to Ansible Server') {
      steps {
        sh '''
          ssh ansible@172.31.82.65 "rm -rf ~/ansible-jenkins-deployment"
          scp -r . ansible@172.31.82.65:~/ansible-jenkins-deployment
        '''
      }
    }

    stage('Trigger Ansible Playbook') {
      steps {
        sh '''
          ssh ansible@172.31.82.65 "cd ~/ansible-jenkins-deployment && ansible-playbook -i inventory/production site.yml"
        '''
      }
    }
  }
}
