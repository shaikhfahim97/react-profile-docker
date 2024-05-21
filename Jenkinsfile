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
        sh "argocd app create guestbook --repo https://github.com/shaikhfahim97/react-profile-docker.git --path production --dest-server https://kubernetes.default.svc --dest-namespace argocd-app"
      }
    }
    
  }
}
