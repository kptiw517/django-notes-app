pipeline {
    agent any
    
    stages {
        stage("clone Code"){
            steps {
               echo "cloning the code"  
               git url:"https://github.com/kptiw517/django-notes-app.git", branch: "main"
            }
           
        }
        
        stage("build"){
            steps {
                echo "building the code"
                sh "docker build -t notes-app ."
            }
        }
        
        stage("push to docker hub"){
            steps {
                echo "pushing the image to the docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub" ,passwordVariable:"dockerHubPass" ,usernameVariable:"dockerHubUser")]){
                sh "docker tag myfirst_app ${env.dockerHubUser}/notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                }
            }
        }
        
        stage("Deploying the app"){
            steps {
                echo "deploying the app"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
