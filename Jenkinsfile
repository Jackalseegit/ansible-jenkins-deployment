pipeline {
  agent any

  stages {
    stage('Checkout Git') {
      steps {
        git branch: 'main',
            credentialsId: 'your-git-creds-id',
            url: 'git branch: 'main', credentialsId: 'abe97d2c-9bcd-4614-bcb5-b23d66d13ca9', url: 'https://github.com/Jackalseegit/ansible-jenkins-deployment.git''
      }
    }

    stage('Copy to Ansible Server') {
      steps {
        sh '''
          ssh ansible@172.31.23.81 "rm -rf ~/ansible-jenkins-deployment"
          scp -r . ansible@172.31.23.81:~/ansible-jenkins-deployment
        '''
      }
    }

    stage('Trigger Ansible Playbook') {
      steps {
        sh '''
          ssh ansible@172.31.23.81 "cd ~/ansible-jenkins-deployment && ansible-playbook -i inventory/production site.yml"
        '''
      }
    }
  }
}
