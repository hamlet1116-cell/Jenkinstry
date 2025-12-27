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
    }
    
    stage('Build Docker') {
      steps {
        sh 'docker build -t my-nginx .'
      }
    }
    
    stage('Run Docker') {
      steps {
        // Stop the old container if it exists
        sh 'docker ps -q -f name=my-nginx | grep -q . && docker stop my-nginx || echo "No running container"'

        // Remove the old container if it exists
        sh 'docker ps -a -q -f name=my-nginx | grep -q . && docker rm my-nginx || echo "No old container to remove"'

        // Run the new container on port 8080
        sh 'docker run -d -p 8080:80 --name my-nginx my-nginx'
      }
    }
  }
}
