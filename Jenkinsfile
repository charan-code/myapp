node{
    stage('SCM Checkout'){
        git 'https://github.com/javahometech/my-app'
    }

 stage('MVN Package'){
     sh label: '', script: 'mvn clean package'
    }
 stage('Build Docker Image'){
     sh 'sudo docker build -t 40008639/my-app:2.0.0 .'
 }
 stage('Push Docker Image'){
     withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubpwd')]) {
         sh "docker login -u 40008639 -p ${dockerHubpwd}"
     }
     sh 'docker push 40008639/my-app:2.0.0'
 }
 stage('Run container'){
     def dockerRun = 'docker run -p 8080:8088 -d -name my-app 40008639/my-app:2.0.0'
 }
}
