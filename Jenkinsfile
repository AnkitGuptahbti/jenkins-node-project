pipeline {
    agent any

    stages {
        stage('Clone Repo') {
            steps {
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    }

    post {
        success {
            echo "Build Success!"
        }
        failure {
            echo "Build Failed!"
        }
    }
}
