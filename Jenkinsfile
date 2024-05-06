pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
       checkout scm
      }
    }

    stage('build') {
      steps {
        docker build -t profile-react .
      }
    }

    stage('deploy') {
      steps {
        argocd app create guestbook --repo https://github.com/argoproj/argocd-example-apps.git --path production --dest-server https://kubernetes.default.svc --dest-namespace rect-profile
      }
    }
  }
}

