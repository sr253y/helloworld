
	pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                checkout scm
            }
        }

	stage('Build Docker Image') {
		steps {
			// Clone the Git repository containing the Dockerfile
			git url: 'https://github.com/sr253y/helloworld.git'
        
			// Build the Docker image using the Dockerfile from the cloned repository
        script {
            docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                def imageName = "sr253y/helloworld:latest"
                def dockerImage = docker.build(imageName, '.')
                dockerImage.push()
            }
        }
    }
}

    stage('Run Docker Container') {
        steps {
            // Run the Docker container
            script {
				docker.image("sr253y/helloworld:latest").run("-p 28080:28080")
                }
            }
        }
    }
}

