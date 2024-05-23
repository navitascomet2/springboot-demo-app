pipeline {
    agent any

    environment {
        registry = "891377337960.dkr.ecr.us-east-1.amazonaws.com/springboot-demo-app"
    }
    
    tools{
        jdk 'jdk17'
        maven 'Maven3'
    }
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'develop', changelog: false, poll: false, url: 'https://github.com/navitascomet2/springboot-demo-app.git'
            }
        }

        stage("Compile"){
            steps{
                sh "mvn clean compile"
            }
        }

         stage("Test Cases"){
            steps{
                sh "mvn test"
            }
        }

        stage("Sonarqube Analysis "){
            steps{
                withSonarQubeEnv('sonar-server') {
                    // sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=navitascomet2_springboot-demo-app_7a1fdab9-4d6f-4f4a-8e85-d5d999212250 -Dsonar.projectName='springboot-demo-app'"
                    sh "mvn clean package"
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=springboot-demo-app \
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectKey=springboot-sonar '''                    
                }
            }
        }
        
        // stage("Quality Gate") {
        //     steps {
        //       timeout(time: 5, unit: 'MINUTES') {
        //         waitForQualityGate abortPipeline: true
        //       }
        //     }
        // }


        stage('OWASP Dependency-Check Vulnerabilities') {

            steps {
                dependencyCheck additionalArguments: ''' 
                            -o './'
                            -s './'
                            -f 'ALL' 
                            --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
        
         stage("Build"){
            steps{
                sh " mvn clean install"
            }
        }

        stage ("Docker build") {
            steps {
                script {
                    dockerImage = docker.build registry
                }
                // sh "docker build -t demoapp ."

            }
        }
        
        // stage("Docker Build & Push"){
        //     steps{
        //         script{
        //            withDockerRegistry(credentialsId: '58be877c-9294-410e-98ee-6a959d73b352', toolName: 'docker') {
                        
        //                 sh "docker build -t image1 ."
        //                 sh "docker tag image1 adijaiswal/pet-clinic123:latest "
        //                 sh "docker push adijaiswal/pet-clinic123:latest "
        //             }
        //         }
        //     }
        // }
        
        // stage("TRIVY"){
        //     steps{
        //         sh " trivy image adijaiswal/pet-clinic123:latest"
        //     }
        // }
        
        // stage("Deploy To Tomcat"){
        //     steps{
        //         sh "cp  /var/lib/jenkins/workspace/CI-CD/target/petclinic.war /opt/apache-tomcat-9.0.65/webapps/ "
        //     }
        // }
    }
}
