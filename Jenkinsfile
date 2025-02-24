pipeline {
    agent any
    environment {
        EC2_SSH_KEY = credentials('id_rsa')
        ANSIBLE_HOST_KEY_CHECKING = 'False'
       
    }

    stages {
        stage('Prepare SSH') {
            steps {
                sh 'mkdir -p ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts'
            }
        }
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/SkyD0ge/jenkin_practice.git', branch: 'main'
		}
        }
        stage('Deploy Website') {
            steps {
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
    }
}

