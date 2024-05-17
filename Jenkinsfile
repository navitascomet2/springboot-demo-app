pipeline {
   tools {
        maven 'Maven3'
    }
    agent any
    environment {
        registry = "891377337960.dkr.ecr.us-east-1.amazonaws.com/navitas-spring-boot-2"
    }
   
    stages {
        stage('Cloning Git') {
            steps {
                git credentialsId: '2a67722f-b565-4098-a029-ed6bb84aa768', url: 'https://github.com/navitascomet2/springboot-demo-app'   
            }
        }
      stage ('Build') {
          steps {
            sh 'mvn clean install'           
            }
      }
    // Building Docker images
    // stage('Building image') {
    //   steps{
    //     script {
    //       dockerImage = docker.build registry 
    //     }
    //   }
    // }
   
    // Uploading Docker images into AWS ECR
    // stage('Pushing to ECR') {
    //  steps{  
    //      script {
    //             sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 891377337960.dkr.ecr.us-east-1.amazonaws.com/navitas-spring-boot-2'
    //             sh 'docker push 891377337960.dkr.ecr.us-east-1.amazonaws.com/navitas-spring-boot-2:latest'
    //      }
    //     }
    //   }

    //    stage('K8S Deploy') {
    //     steps{   
    //         script {
    //             withKubeConfig([credentialsId: 'K8S', serverUrl: '']) {
    //             sh ('kubectl apply -f  eks-deploy-k8s.yaml')
    //             }
    //         }
    //     }
    //    }
    }
}