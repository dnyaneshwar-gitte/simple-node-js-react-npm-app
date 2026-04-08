// pipeline {
//     agent any

//     tools {
//         nodejs 'NodeJS-18'
//     }

//     environment {
//         DOCKER_IMAGE = "dnyaneshwar535/node-react-app"
//     }

//     stages {

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

//         stage('Build App') {
//             steps {
//                 sh 'npm run build'
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 script {
//                     docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
//                 }
//             }
//         }

//         stage('Push Docker Image') {
//             steps {
//                 script {
//                     docker.withRegistry('', 'docker-creds') {
//                         docker.image("${DOCKER_IMAGE}:${BUILD_NUMBER}").push()
//                     }
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             emailext (
//                 subject: "SUCCESS: Build #${BUILD_NUMBER}",
//                 body: "Pipeline succeeded!",
//                 to: "dnyaneshwarg535@gmail.com"
//             )
//         }

//         failure {
//             emailext (
//                 subject: "FAILED: Build #${BUILD_NUMBER}",
//                 body: "Pipeline failed!",
//                 to: "dnyaneshwarg535@gmail.com"
//             )
//         }
//     }
// }



pipeline {
    agent any

    tools {
        nodejs 'node20'
    }

    environment {
        DOCKER_IMAGE = "dnyaneshwar535/node-react-app"
        TAG = "${BUILD_NUMBER}"
    }

    stages {


        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test'
            }
        }

        stage('Build App') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %DOCKER_IMAGE%:%TAG% .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %DOCKER_IMAGE%:%TAG%'
            }
        }
        stage('Deploy Staging') {
            when {
                branch 'develop'
            }
            steps {
                echo "Deploying to STAGING"
            }
        }

        stage('Deploy Production') {
            when {
                branch 'main'
            }
            steps {
                echo "Deploying to PRODUCTION"
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: Jenkins Pipeline",
                body: "Build Successful!",
                to: "dnyaneshwarg535@gmail.com"
            )
        }
        failure {
            emailext (
                subject: "FAILED: Jenkins Pipeline",
                body: "Build Failed!",
                to: "dnyaneshwarg535@gmail.com"
            )
        }
    }
}