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
                git url: 'https://github.com/SkyD0ge/jenkin_practice.git', branch: 'main'
		}
        }
        stage('Deploy Website') {
            steps {
               withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                    sh 'ansible-playbook -i inventory playbook.yml'
                }
            }
        }
    }
}

