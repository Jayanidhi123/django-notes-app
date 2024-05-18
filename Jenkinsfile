pipeline {
    agent any 
     environment {
        DOCKER_CREDENTIALS = 'dockerHub'
        DOCKER_IMAGE_NAME = 'my-note-app'
        DOCKER_HUB_USERNAME = 'jayasree1061'
        DOCKER_HUB_PASSWORD = "Sreenidhi123@"
    }
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/Jayanidhi123/django-notes-app.git", branch: "main"
            }
        }
       stage("Build") {
            steps {
                echo "Building the image"
                script {
                    // docker.build(DOCKER_IMAGE_NAME)
                     bat 'docker build -t my-note-app .'
                }
            }
        }

       stage("Push to Docker Hub") {
    steps {
        echo "Pushing the image to Docker Hub"
        withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS, passwordVariable: 'DOCKER_HUB_PASSWORD', usernameVariable: 'DOCKER_HUB_USERNAME')]) {
            script {
                docker.withRegistry('https://hub.docker.com', DOCKER_HUB_USERNAME, DOCKER_HUB_PASSWORD) {
                    docker.image my-note-app.push()
                }
            }
        }
    }
}

    }
}
