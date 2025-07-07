pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-hello-world"
        CONTAINER_NAME = "flask-container"
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/Sarthak-1-8/AutoDock-CI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // agar container exit karta hai then remove it
                    sh "docker rm -f $CONTAINER_NAME || true"
                    sh "docker run -d --name $CONTAINER_NAME -p 5000:5000 $IMAGE_NAME"
                    // Schedule removal after 7 days
                    sh "echo 'docker rm -f $CONTAINER_NAME' | at now + 10080 minutes"
                }
            }
        }

        stage('Log Success') {
            steps {
                writeFile file: 'deploy.log', text: "triggeredok\n"
                sh 'cat deploy.log'
            }
        }
    }
}

