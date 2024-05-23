pipeline {
  agent any
  
  stages {
    
    stage('Checkout') {
      steps {
       checkout scm
      }
    }
    stage('build & push ') {
      steps {
        script {
          withDockerRegistry(credentialsId: '6b0c28c1-dfe6-4784-a5fe-a0785abd754b') {
            sh "docker build -t shaikhfahim97/react-repo:rect2 ."
            sh "docker push shaikhfahim97/react-repo:rect2"
            
          }
        }
      }
    }
    
    stage('deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: '615eb985-396e-445e-bb98-e26e2da0d2c8', passwordVariable: 'password', usernameVariable: 'username')]) {
          // some block
          sh "argocd login localhost:8090 --username $username --password $password"
          sh "argocd app create guestbook --repo https://github.com/shaikhfahim97/react-profile-docker.git --path production --dest-server https://kubernetes.default.svc --dest-namespace argocd-app"
          }  
        }
    }
    
  }
}
