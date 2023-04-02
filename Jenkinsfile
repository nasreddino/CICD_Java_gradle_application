pipeline {
    agent any 
    stages {
        
        stage("docker build & docker push"){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_pass', variable: 'docker_password')]) {
                             sh '''
                                docker build -t 172.18.0.3:8083/javaapp .
                                docker login -u admin -p @nexus123 172.18.0.3:8083 
                                docker push  172.18.0.3:8083/javaapp
                                docker rmi 172.18.0.3:8083/javaapp
                            '''
                    }
                }
            }
        }
        
    }
}
