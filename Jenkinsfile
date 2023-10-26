pipeline {
    agent { label 'Dev_Agent'}
   
    stages{
        stage("Code"){
            steps {
                git url: "https://github.com/suhasiForDevOps22/node-todo-cicd.git", branch: "master"
            }
           
        }
        stage("Build and Test"){
            steps {
                echo "Building and testing"
                sh 'docker build . -t suhasig/node-todo-app-cicd:latest'
            }
           
        }    
        stage("Push"){
            steps {
                echo "Pushing image"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"   
                sh "docker push suhasig/node-todo-app-cicd:latest"
                }
               
            }
           
        }
        stage("Deploy"){
            steps {
                echo "Deploying"
                sh 'docker-compose down && docker-compose up -d'
           
            }
           
        }
    }
   
}
