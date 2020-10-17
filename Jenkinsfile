node{
     
    stage('SCM Checkout'){
        git credentialsId: 'GIT_CREDENTIALS', url: 'https://github.com/arjun1128/neudesic.git',branch: 'main'
    }
    
    
    stage('Build Docker Image'){
        sh 'docker build -t arjunps/php-mysql .'
    }
    
    stage('Push Docker Image'){
        withCredentials([string(credentialsId: 'DOCKER_HUB_CREDENTIALS', variable: 'DOCKER_HUB_CREDENTIAL')])
         {
          sh "docker login -u arjunps -p ${DOKCER_HUB_CREDENTIAL}"
        }
        sh 'docker push arjunps/php-mysql'
     }
     
     stage("Deploy To Kuberates Cluster"){
        sh 'kubectl apply -f springBootMongo.yml'
      } 
     
}
