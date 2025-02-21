pipeline {
    agent any
    
    environment {
        // Using SSH key stored in Jenkins credentials
        EC2_SSH_KEY = credentials('EC2_SSH')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
       
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout scm
            }
        }

        stage('Run Ansible Playbook') {
            steps {
                script {
                    // Running Ansible Playbook to configure the server
                    sh '''
ansible-playbook -i ./ansible/inventory.aws_ec2.yml -e 'host_group=tag_git_gitaction' ./ansible/playbooks/nginx-setup.yml -u ubuntu --private-key $EC2_SSH_KEY
                    '''
                }
            }
        }
    }
}

