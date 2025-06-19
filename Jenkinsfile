pipeline {
    agent {
        docker {
            image 'docker:latest'  // Use a Docker CLI image
            args '-v /var/run/docker.sock:/var/run/docker.sock -e HOME=/home/appadmin/Desktop/jenkins' // Access host Docker
        }
    }

    environment {
        IMAGE_NAME = 'myimage' // We'll tag the image with this name
    }

    stages {

        // 👇 This stage pulls your Git repo code into the Jenkins workspace
        stage('Checkout Code') {
            steps {
                // git branch: 'main', url: 'https://github.com/Soni8945/cicd-pipeline'
                // ⬇️ This is where Jenkins pulls from the Git repository (defined in Jenkins Job UI)
                checkout scm
            }
        }

        // 👇 Build Docker image using the Dockerfile from the pulled repo
        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $IMAGE_NAME ." // Builds image from current directory
                }
            }
        }

        // 👇 Run the built Docker container
        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run --rm $IMAGE_NAME" // Runs the image and removes the container after
                }
            }
        }
    }
}