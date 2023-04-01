pipeline {
    agent any 
    stages {
        
        stage("sonar quality check") {
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonar-pass') {
                            sh 'chmod +x gradlew'
                            sh './gradlew sonarqube'
                    }

                    timeout(time: 1, unit: 'HOURS') {
                      def qg = waitForQualityGate()
                      if (qg.status != 'OK') {
                           error "Pipeline aborted due to quality gate failure: ${qg.status}"
                      }
                    }

                }  
            }
        }
        
        stage("docker build & docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                             sh '''
                                docker build -t 172.18.0.3:8083/javaapp:${VERSION} .
                                docker login -u admin -p $docker_password 172.18.0.3:8083 
                                docker push  172.18.0.3:8083/javaapp:${VERSION}
                                docker rmi 172.18.0.3:8083/javaapp:${VERSION}
                            '''
                    }
                }
            }
        }
        
    }
}
