pipeline {
    agent any
    tools{
        maven 'maven'
    }

    stages {
        stage('Build Maven') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Lakshmansai1999/devops-automation.git']])
                sh 'mvn clean install'
            }
        }
        
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t lakshmansai/kubernetes .'
                }
            }
        }
        
        withCredentials([string(credentialsId: 'dockerpwd', variable: 'dockerhubpwd')]) {
            sh 'docker login -u lakshmansai -p ${dockerhubpwd}'
        }
        sh 'docker push lakshmansai/kubernetes'
    }
}
