// pipeline {
//     agent any

//     stages {

//         stage('Install Dependencies') {
//             steps {
//                 sh 'npm install'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 sh '''
//                 docker build -t my-k8s-app:${BUILD_NUMBER} .
//                 docker tag my-k8s-app:${BUILD_NUMBER} akshayareddy23/my-k8s-app:${BUILD_NUMBER}
//                 '''
//             }
//         }

//         stage('Push Docker Image') {
//             steps {
//                 withCredentials([usernamePassword(
//                     credentialsId: 'dockerhub-creds',
//                     usernameVariable: 'DOCKER_USER',
//                     passwordVariable: 'DOCKER_PASS'
//                 )]) {
//                     sh '''
//                     echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
//                     docker push akshayareddy23/my-k8s-app:${BUILD_NUMBER}
//                     '''
//                 }
//             }
//         }
//     }
// }
pipeline {
    agent any

    stages {

        stage('Checkout from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/AkshayaReddyDubbaka/k8s-lab.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t k8s-lab:${BUILD_NUMBER} .'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 3000:8080 k8s-lab:${BUILD_NUMBER}'
            }
        }

    }
}
