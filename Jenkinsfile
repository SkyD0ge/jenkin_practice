pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                sshagent(credentials: ['ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIBZcP5G0bcehllXstWJNHT5cdHL+oQWqml/LAGDv5WHc aakash.sahani@outlook.com
']) {
                    git url: 'git@github.com:SkyD0ge/jenkin_practice.git', branch: 'main'
            }
        }
        stage('Deploy Website') {
            steps {
                sh 'ansible-playbook -i inventory deploy_website.yml'
            }
        }
    }
}
