pipeline {
    agent any
    triggers {
        githubPush()
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
    post {
        failure {
            emailext (
                subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "The build has failed. Please review the console output here: ${env.BUILD_URL}",
                to: "aakash.sahani@ubuy.com"
            )
            echo "Build failed – initiating rollback to previous build..."
            withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                sh 'ansible-playbook -i inventory rollback.yml'
            }
        }
    }
}

