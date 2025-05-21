pipeline {
    agent any

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'master', url: 'https://github.com/Vishnupriyalnm/healthcare.git'
                sh 'mvn clean package'
            }
        }
        stage('Build docker image') {
            steps {
                sh 'docker build -t vishnupriyalnm/healthcaredemo:1 .'
            }
        }
        stage('Docker image to dockerhub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhubpass', variable: 'dockerhubpass')]) {
                 sh "docker login -u  vishnupriyalnm -p ${dockerhubpass}"
                 sh "docker push vishnupriyalnm/healthcaredemo:1"
}
            }
        }
        stage('deploy using kubernetes') {
            steps {
                sh 'sudo kubectl apply -f kubernetesfile.yml'
                sh 'sudo kubectl get all'
            }
        }
    }
}
