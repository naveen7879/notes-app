pipeline {
    agent any 

    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/naveen7879/notes-app.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUSer} -p ${env.dockerHubpass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the comtainer"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
