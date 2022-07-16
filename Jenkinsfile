pipeline {
    agent any
    tools{
        maven 'M2_HOME'
    }
    stages {
        stage('Checkout'){
            steps{
                git branch: 'main', url: 'https://github.com/dieunor/geolocation.git'
            }
        }
        stage('Code Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }
}
  // Building Docker images
        stage('Building image') {
            steps{
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        // Uploading Docker images into AWS ECR
        stage('Pushing to ECR') {
            steps{
                script {
                    sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin 932663817409.dkr.ecr.ap-south-1.amazonaws.com'
                    sh 'docker push 932663817409.dkr.ecr.ap-south-1.amazonaws.com/geolocation_ecr_rep2:latest'
                }
            }
        }
