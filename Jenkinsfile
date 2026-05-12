pipeline {
    agent {
        label "node1"
    }

    stages {

        stage("Checkout") {
            steps {
                checkout scm
            }
        }

        stage("Build Docker Image") {
            steps {
                echo "Building Docker Image"
                sh "docker build -t python-app ."
            }
        }

        stage("Stop Old Container") {
            steps {
                echo "Stopping old container if exists"
                sh "docker stop python-container || true"
            }
        }

        stage("Remove Old Container") {
            steps {
                echo "Removing old container if exists"
                sh "docker rm python-container || true"
            }
        }

        stage("Run New Container") {
            steps {
                echo "Running new container"
                sh """
                    docker run -d -p 8001:8000 --name python-container python-app
                """
            }
        }
    }
    
    post {
        success {
            echo "Deployment Successful 🚀"
        }
        failure {
            echo "Deployment Failed ❌"
        }
    }
}