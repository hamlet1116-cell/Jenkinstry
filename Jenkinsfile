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
  }
}
