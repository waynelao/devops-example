pipeline {
    agent any
    tools{
        maven 'maven_3_9_1'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/waynelao/devops-example']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t mhyx/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'RealDockerHubpwd', variable: 'dockerhubpwd')]) {
                        sh 'docker login -u mhyx -p ${dockerhubpwd}'
}
                        sh 'docker push mhyx/devops-integration'
                }
            }
        }
    }
}