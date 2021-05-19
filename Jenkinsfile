pipeline {
    agent any
    tool name: 'MyNodeJS', type: 'nodejs'
    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
                nodejs('MyNodeJS')
                sh 'npm install'
            }
        }
    }
}
