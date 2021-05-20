pipeline {
environment {
registryCredential = "docker"
}
agent any
stages {
stage(‘Build’) {
    steps{
    script {
        sh 'mvn clean install'
    }
    }
}
stage(‘Load’) {
    steps{
    script {
        app = docker.build("cloud007/simple-spring")
    }
    }
}
    stage(‘Deploy’) {
    steps{
    script {
        docker.withRegistry( "https://registry.hub.docker.com", registryCredential ) {
        // dockerImage.push()
        app.push("latest")
        }
    }
    }
}
stage('Deploy to ACS'){
    steps{
        withCredentials([azureServicePrincipal('dbb6d63b-41ab-4e71-b9ed-32b3be06eeb8')]) {
        sh 'echo "logging in" '
        sh 'az login --service-principal -u **************************** -p ********************************* -t **********************************’
        sh 'az account set -s ****************************'
        sh 'az aks get-credentials --resource-group ilink --name    mycluster'
        sh 'kubectl apply -f sample.yaml'
    }
}
}
}
}