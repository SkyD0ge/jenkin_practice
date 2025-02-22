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
                sshagent(credentials: ['ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCxfVRKUsdlN7iqoOwcc8xVSZP/huGZqMXKNnnPEsU5SvDZUsNniGehiQdVgUIgvxGkyEs4dynr255iXjixRZBY7KnAFoyrFACcBOmxZ7aS5T0gnFiH5YYIsfwQ04mfojX6V+gEA6tENbKwtD6wUKiiR4MkzqlB4F0i2a+PwlMJ80QRDOF97i1TXFsCfwf3hnSgrjYbB3tLS4r4RExU0PbOKL30hhwOYbBDhSO3EVEZ7zrW7EwTlCVQPHQ6LW0OB1hLvd6Wjl3Hi1OOufWi8Va5BDCr9wmTTjsRWYRXlhYmCzpjLt5yBox/k/kkadDC2RQNteJITPU4hjXp629s3A+JaS3rJ79DnnKnr/1Wuo82/DS6RTsH9lbvdW1QvrpY1Ki2G6YV4E1aceA0sl6UC/S9dkTXiwnX53GVjffQWJ0AtPRrg+KREamiidtQkMBMDumY+8Z4HJPYeotbZ9xz9oZPYvD9WkUewiY24OGn7tCQd5TW4RhHC+Wwl+8wH8caYPFU3N/y+8Jphui8lrAuUxeymL3YzJqH9sJgNepCjckE++7Og06Rjtcbcjv1+J/Zg7pdly6Lscd7el+KcPXGEXtQyKKqs8BLkJ5iPWpQ8XH6cYeNk0BFNAIiV21sPKvgHE1eq+CaAG13d1sZS7ZFuDoU8a9p1rPfAbihLjGkj5jtBw== aakash.sahani@outlook.com']) {
                    git url: 'git@github.com:SkyD0ge/jenkin_practice.git', branch: 'main'
            }
        }
        stage('Deploy Website') {
            steps {
                sh 'ansible-playbook -i inventory playbook.yml'
            }
        }
    }
}
