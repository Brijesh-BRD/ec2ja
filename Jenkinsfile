pipeline {
    agent any

    environment {
        ANSIBLE_HOST_KEY_CHECKING = 'False'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Brijesh-BRD/ec2ja.git'  
            }
        }

        stage('Launch EC2') {
            steps {
                sh 'ansible-playbook launch-ec2.yml'
            }
        }

        stage('Wait for EC2 SSH') {
            steps {
                script {
                    sleep(time:60, unit:"SECONDS")  // Give time to boot and be reachable
                }
            }
        }

        stage('Configure Web Server') {
            steps {
                sh 'ansible-playbook -i inventory.ini configure-web.yml'
            }
        }
    }
}
