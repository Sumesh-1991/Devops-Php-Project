pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/Sumesh-1991/Devops-Php-Project.git'
            }
        }


        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test_server', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test_server', playbook: 'python3-playbook.yml'
            }
        }
    }
}

