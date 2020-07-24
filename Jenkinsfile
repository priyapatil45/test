node{
    stage('git checkout'){
        git credentialsId: 'git-creds', url: 'https://github.com/shubhamkushwah123/devops-bootcamp2.git'
    }
    
    stage('code build & test'){
       // sh 'mvn clean package'
       
       def mavenHome = tool name: 'maven-3' , type: 'maven'
       def mavenCMD = "${mavenHome}/bin/mvn"
       sh "${mavenCMD} clean package"
    }
    
    stage('docker build'){
        sh 'docker build -t shubhamkushwah123/cicd-demo:3.0 .'
    }
    
    stage('docker push'){
       withCredentials([string(credentialsId: 'dockerPwd', variable: 'dockerHubPwd')]) {
        sh "docker login -u shubhamkushwah123 -p ${dockerHubPwd}"
        }
        sh 'docker push shubhamkushwah123/cicd-demo:3.0'
    }
    
    stage('docker run'){
        sh 'docker run -p 8888:8082 -d shubhamkushwah123/cicd-demo:3.0'
    }
}