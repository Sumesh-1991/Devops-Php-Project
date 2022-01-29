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
        stage('Docker Push'){
        steps{
        withDockerRegistry(credentialsId: 'docker-hub', url: 'https://hub.docker.com/repository/docker/sumesh1991/') {
                              sh "docker push sumesh/my-php-website:latest"
                 }
             }
        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook  credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

