pipeline {
    agent any

    stages {
        stage('Clone Code') {
            steps {
               git branch: 'main', url: 'https://github.com/Sumesh-1991/Devops-Php-Project.git'
            }
        }
        stage('Docker Build'){
            steps{
                sh "docker build . -t sumesh/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                
                withCredentials([string(credentialsId: 'docker-hub-cred')]) {
                      sh "docker login -u sumesh1991 -p 6df67116-909d-49e8-9b26-a41788ee0dd3"
                }
                
                sh "docker push sumesh/my-php-website:latest "
            }
        }


        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'centos', installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'centos', installation: 'Ansible', inventory: 'servers.ini', playbook: 'python3-playbook.yml'
            }
        }
    }
}

