pipeline {
    agent any 
    stages {
        
        stage("docker build & docker push"){
            steps{
                script{
                             sh 'docker build -t 172.18.0.3:8083/javaapp .'
                             sh 'docker login -u admin -p @nexus123 172.18.0.3:8083' 
                             sh 'docker push  172.18.0.3:8083/javaapp'
                             sh 'docker rmi 172.18.0.3:8083/javaapp'
                }
            }
        }
        
    }
}
