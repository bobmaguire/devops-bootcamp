pipeline {
    agent any

    tools {
        nodejs 'MyNodeJS'
    }
    stages {
 
        stage('build') {
            steps {
                sh 'npm install'
            }
        }
        stage('test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Docker Image Build') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'MyDockerRepo', passwordVariable: 'AWS_SECRET_ACCESS_KEY', usernameVariable: 'AWS_ACCESS_KEY_ID')]) {
                sh '''
                wget https://download.docker.com/linux/ubuntu/dists/bionic/pool/stable/amd64/docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                dpkg -i ./docker-ce-cli_18.09.9~3-0~ubuntu-bionic_amd64.deb
                apt-get update
                apt-get install -y awscli
                docker build -t workshopuser15:latest .
                docker tag workshopuser15:latest workshopuser15:${BUILD_NUMBER}
                docker tag workshopuser15:latest 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser15:latest
                $(aws ecr get-login --region us-east-1 | sed 's/-e none//g')
                docker push 686567993080.dkr.ecr.us-east-1.amazonaws.com/devopsbootcampuser15:latest
                ''' 
            }
        }
    }     
}