@Library('Shared') _

pipeline{
    agent{ label 'linux' }

    stages{

        stage('Welcome Message'){
            steps {
                script {
                    welcome()
                }
            }
        }

        stage('Code Clone(GitHub)'){
            steps{
                script {
                    checkout_code('https://github.com/impankaj91/jenkins-pipeline-sampleapp.git','main')
                }
            }
        }

        stage('Build (Docker)'){
            steps{
                script{
                    docker_build('note-app','latest')
                }
            }
        }

        stage('Push Image (DockerHub)'){
            steps{
                script {
                    docker_push('DockerHub','note-app','latest')
                }
            }
        }

        stage('Deploy'){
            steps{
                script{
                    docker_deploy()
                }
            }
        }
    }
}