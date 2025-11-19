// pipeline {
//     agent any

//     stages {
//         stage('Clone Repo') {
//             steps {
//                 checkout scm
//             }
//         }

//         stage('Install Dependencies') {
//             steps {
//                 sh 'npm install'
//             }
//         }

//         stage('Run Tests') {
//             steps {
//                 sh 'npm test'
//             }
//         }
//     }

//     post {
//         success {
//             echo "Build Success!"
//         }
//         failure {
//             echo "Build Failed!"
//         }
//     }
// }

pipeline {
  agent any
  stages {
    stage('Checkout') { steps { checkout scm } }
    stage('Install')  { steps { sh 'npm install' } }
    stage('Test')     { steps { sh 'npm test' } }

    stage('Build Image') {
      steps { sh 'docker build -t ankit/node-app:latest .' }
    }

    stage('Deploy Container') {
      steps {
        sh '''
          docker stop node-app || true
          docker rm node-app || true
          docker run -d --name node-app -p 3000:3000 ankit/node-app:latest
        '''
      }
    }
  }
  post {
    success { echo "CI/CD with Docker complete" }
    failure { echo "Build/Deploy failed" }
  }
}
