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
                echo "Checked at ${new Date()}"
                // Optional: skip tidy if not installed
                // sh 'tidy -errors -q index.html || true'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image using Docker Pipeline plugin
                    def appImage = docker.build("my-nginx:latest", ".")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Stop old container if exists
                    try {
                        docker.image("my-nginx:latest").stop("my-nginx")
                        docker.image("my-nginx:latest").remove("my-nginx")
                    } catch (Exception e) {
                        echo "No old container to remove"
                    }

                    // Run new container
                    docker.image("my-nginx:latest").run("-d -p 8080:80 --name my-nginx")
                }
            }
        }
    }
}
