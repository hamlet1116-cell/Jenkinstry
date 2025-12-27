pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    
    stage('Validate HTML') {
      steps {
        sh 'echo "Checked at $(date)"'
        sh 'tidy -errors -q index.html || true'
        
      }
     stage('Build Docker') {
      steps {
        sh 'docker build -t my-nginx .'
      }
    }
    stage('Run Docker') {
      steps {
        sh 'docker stop my-nginx || true'
        sh 'docker rm my-nginx || true'
        sh 'docker run -d -p 8081:80 --name my-nginx my-nginx'
      }
    }
  }
}
