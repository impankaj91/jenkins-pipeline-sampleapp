pipeline{
    agent{ label 'linux' }
    stages{
        stage('Clone the code from the repo'){
            steps{
                echo 'Cloning the code from the repo'
                git branch: 'main', url: 'https://github.com/impankaj91/jenkins-pipeline-sampleapp.git'
            }
        }

        stage('Build Code using the Docker'){
            steps{
                echo 'Building the docker image'
                sh 'docker build -t note-app:latest .'
            }
        }

        stage('Push image to DockerHub'){
            steps{
                withCredentials([usernamePassword(credentialsId:"DockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                echo "Pushing the image to dockerhub - ${env.dockerHubUser}"
                sh """
                docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}
                docker tag note-app:latest ${env.dockerHubUser}/note-app:latest
                docker push ${env.dockerHubUser}/note-app:latest 
                """
                }
            }
        }

        stage('Deploy'){
            steps{
            echo 'Deploying code to the server'
            sh 'docker-compose down && docker-compose up -d'}
        }
    }
}