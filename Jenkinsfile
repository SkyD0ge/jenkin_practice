pipeline {
    agent {
        label 'linux'
    }

    environment {
        BUILD_ID = sh(script: "git log --pretty=format:'%h' -n 1", returnStdout: true).trim()
        PREV_BUILD_ID = sh(script: "git log --pretty=format:'%h' -n 2 | tail -n1", returnStdout: true).trim()
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/SkyD0ge/jenkin_practice.git' 
            }
        }

        stage('Deploy Application') {
            steps {
                withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                    sh "ansible-playbook -i inventory playbook.yml --extra-vars 'build_id=${BUILD_ID}'"
                }
            }
        }
    }

    post {
        failure {
            emailext(
                subject: "Jenkins Build Failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed. Rolling back...",
                to: "aakash.sahani@ubuy.com"
            )

            echo "Build failed – rolling back to previous stable commit ${PREV_BUILD_ID}..."

            withEnv(["ANSIBLE_HOST_KEY_CHECKING=False"]) {
                sh "ansible-playbook -i inventory playbook.yml --extra-vars 'rollback=true build_id=${PREV_BUILD_ID}'"
            }
        }

        success {
            emailext(
                subject: "Jenkins Build Succeeded: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build succeeded. Running on commit: ${BUILD_ID}",
                to: "aakash.sahani@ubuy.com"
            )
        }
    }
}

