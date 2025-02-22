pipeline {
    agent any
    stages {
        stage('Prepare SSH') {
            steps {
                sh 'mkdir -p ~/.ssh && ssh-keyscan github.com >> ~/.ssh/known_hosts'
            }
        }
        stage('Checkout Code') {
            steps {
                // Replace 'github-ssh-key' with your credential ID stored in Jenkins
                sshagent(credentials: ['github-ssh-key']) {
                    git url: 'git@github.com:SkyD0ge/jenkin_practice.git', branch: 'main'
                }
            }
        }
        stage('Deploy Website') {
            steps {
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
    }
}

