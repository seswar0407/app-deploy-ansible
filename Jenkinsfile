pipeline {
  agent any


  environment {
   ANSIBLE_INVENTORY = "inventory/hosts.ini"
   PLAYBOOK = "playbooks/deploy.yml"

  }

  stages {
   stage('Checkout') {
    steps {
     echo 'Cloning repo...'
     checkout scm
    }
   }
   
   stage('Run Asible') {
    steps {
      echo 'Running ansible playbook using SSH key from Jenkins credentials...'
      sshagent(['ansible-ssh-key']) {
     sh """
      ansible --version
      ansible-playbook -i $
{ANSIBLE_INVENTORY} ${PLAYBOOK} -v
     """
  
      }
    }
   }
  post {
   success {
    echo 'Deployement successfull..!'
   }
   failure {
    echo 'Deployement failed. Checked console output.'
   }
  }
}
