// pipeline {
//     agent any
//     environment {
//         AWS_REGION = 'eu-west-1' 
//     }
//     stages {
//         stage('Set AWS Credentials') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'Jenkins' 
//                 ]]) {
//                     sh '''
//                     echo "AWS_ACCESS_KEY_ID: $AWS_ACCESS_KEY_ID"
//                     aws sts get-caller-identity
//                     '''
//                 }
//             }
//         }
//         stage('Checkout Code') {
//             steps {
//                 git branch: 'main', url: 'https://github.com/Scoobymike04/class6.git' 
//             }
//         }
//         stage('Initialize Terraform') {
//             steps {
//                 sh '''
//                 terraform init
//                 '''
//             }
//         }
//         stage('Plan Terraform') {
//             steps {
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'Jenkins'
//                 ]]) {
//                     sh '''
//                     export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
//                     export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
//                     terraform plan -out=tfplan
//                     '''
//                 }
//             }
//         }
//         stage('Apply Terraform') {
//             steps {
//                 input message: "Approve Terraform Apply?", ok: "Deploy"
//                 withCredentials([[
//                     $class: 'AmazonWebServicesCredentialsBinding',
//                     credentialsId: 'Jenkins'
//                 ]]) {
//                     sh '''
//                     export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
//                     export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
//                     terraform apply -auto-approve tfplan
//                     '''
//                 }
//             }
//         }
//     }
//     post {
//         success {
//             echo 'Terraform deployment completed successfully!'
//         }
//         failure {
//             echo 'Terraform deployment failed!'
//         }
//     }
// }
pipeline{
    agent any
    tools {
        jfrog 'jfrog_cli'
    }
    stages {
        stage ('Testing') {
            steps {
                jf '-v' 
                jf 'c show'
                jf 'rt ping'
                sh 'touch test-file'
                jf 'rt u test-file Jfrog_cli/'
                jf 'rt bp'
                jf 'rt dl Jfrog_cli/test-file'
            }
        } 
    }
}
