pipeline {
    agent any
    stages {
        stage("Clean Workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Clone") {
            steps {
                git url:"https://github.com/zohaibwarraich1/full-stack_chatApp.git", branch: "main"
                echo "Successfully Cloned!"
            }
        }
        stage("Build") {
            steps {
                sh 'docker build -t fullstack-chatapp-frontend:latest ./frontend/'
                sh 'docker build -t fullstack-chatapp-backend:latest ./backend/'
                echo 'Successfully Build!'
            }
        }
        stage("Push") {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo "$PASSWORD" | docker login -u "$USERNAME" --password-stdin'
                    sh 'docker tag fullstack-chatapp-frontend:latest zohaibwarraich/fullstack-chatapp-frontend:latest'
                    sh 'docker push zohaibwarraich/fullstack-chatapp-frontend:latest'
                    sh 'docker tag fullstack-chatapp-frontend:latest zohaibwarraich/fullstack-chatapp-backend:latest'
                    sh 'docker push zohaibwarraich/fullstack-chatapp-backend:latest'
                    
                }
                echo 'Successfully Pushed!'
            }
        }
        stage("Deploy") {
            steps {
                sh "docker-compose up -d"
                echo 'Successfully Deployed!'
            }
        }
    }
}
