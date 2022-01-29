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
                sh "docker build . -t sumesh1991/my-php-website"
            }
        }
        stage('DockerHub Push'){
            steps{
                withCredentials([string(credentialsId: 'sumesh1991', variable: 'docker')]) {
                      sh "docker login -u sumesh1991 -p ${docker}"
                }            
                  sh "docker push sumesh1991/my-php-website:latest "
            }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test_server', installation: 'Ansible', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test_server', installation: 'Ansible', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

