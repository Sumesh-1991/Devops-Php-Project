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
                
                  sh "docker login -u sumesh1991 -p 45098ed2-9366-40c4-92ad-bb1c0e45304b"
                  sh "docker push sumesh/my-php-website:latest"
            }

        }
        stage('Install Python 3') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'python3-playbook.yml'
            }
        }
         stage('Install docker and its dependencies and run contianer') {
            steps {
               ansiblePlaybook credentialsId: 'test-server', installation: 'ansible', inventory: 'servers.inv', playbook: 'deployment-playbook.yml'
            }
        }
    }
}

