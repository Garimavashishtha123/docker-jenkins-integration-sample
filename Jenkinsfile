pipeline {
    agent any
    tools{
        maven 'maven_3_6_3'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/maater']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Garimavashishtha123/automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t garimavashishtha/myfirstapplication .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u garimavashishtha -p ${dockerhubpwd}'

}
                   sh 'docker push garimavashishtha/myfirstapplication'
                }
            }
        }
      
    }
}