pipeline {
    agent any
    tools{
        maven 'maven3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/irfan041/PipelineIntregation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerpass', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u scgirfan -p ${dockerhubpwd}'

}
                   sh 'docker push scgirfan/devops-integration'
                }
            }
        }
       
    }
}