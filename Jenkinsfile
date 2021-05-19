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
    }
}
