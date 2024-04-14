pipeline {
    agent any
    
    stages{
        stage ("Git") {
            steps{
                git url:'https://github.com/lax66/django-notes-app.git',branch:'main'
            }
        }
        stage ("build") {
            steps {
                sh 'docker build -t todo-app .'
            }
            
        }
        stage ("pushed to dockerHub") {
            steps {
                echo "pushed to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:'dockerHubPass',usernameVariable:'dockerHubUser')]){
                sh "docker tag todo-app ${env.dockerHubUser}/todo-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerhubUser}/todo-app:latest"
                }
            }
        }
        stage ("deployment") {
            steps {
                echo "deployment"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
        
    }
}
