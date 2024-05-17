pipeline {
    agent any 
    
    tools{
        jdk 'jdk11'
        maven 'maven3'
    }
    
    environment {
        SCANNER_HOME=tool 'sonar-scanner'
    }
    
    stages{
        
        stage("Git Checkout"){
            steps{
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/navitascomet2/springboot-demo-app.git'
            }
        }

        stage('Sonar Analysis') {
            steps{
                sh "mvn clean package"
                sh ''' mvn sonar:sonar -Dsonar.url=http://a6a017adc86c74cb68390aa4795aeb85-1012135430.us-east-1.elb.amazonaws.com:9000 -Dsonar.login=squ_69108bc2b4771fa12ead8d2a844cfe158630cc26
                   -Dsonar.java.binaries=. \
                   -Dsonar.projectKey=navitascomet2_springboot-demo-app_7a1fdab9-4d6f-4f4a-8e85-d5d999212250 '''
            }
        }
        
        // stage("Compile"){
        //     steps{
        //         sh "mvn clean compile"
        //     }
        // }
        
        //  stage("Test Cases"){
        //     steps{
        //         sh "mvn test"
        //     }
        // }
        
        // stage("Sonarqube Analysis "){
        //     steps{
        //         withSonarQubeEnv('sonar-server') {
        //             sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=springboot-demo-app \
        //             -Dsonar.java.binaries=. \
        //             -Dsonar.projectKey=springboot-demo-app '''
    
        //         }
        //     }
        // }
        
        // stage("OWASP Dependency Check"){
        //     steps{
        //         dependencyCheck additionalArguments: '--scan ./ --format HTML ', odcInstallation: 'DP'
        //         dependencyCheckPublisher pattern: '**/dependency-check-report.xml'
        //     }
        // }
        
        //  stage("Build"){
        //     steps{
        //         sh " mvn clean install"
        //     }
        // }
        
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
