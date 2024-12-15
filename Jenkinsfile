pipeline {
    agent any
    environment{
        registry_cred = 'DockerCred'
    }
    stages {
        stage('Code') {
            steps {
                echo 'Clone Code Stage'
                git url:"https://github.com/prashik8600/notesapp.git", branch:"main"
                }
            }
        stage('Build') {
            steps {
                echo 'Build Stage'
                sh "docker build -t notesapp2 ."
                }   
            }
        stage('Push') {
            steps {
                
                echo 'Push Stage'
                script{
                    sh "docker tag notesapp2 prashw23/notesapp2:latest"
                    docker.withRegistry('',registry_cred){
                        echo 'Docker Login successfull'
                        // sh "docker push prashw23/notesapp2"
                    }
                }
                // withCredentials([usernamePassword(credentialsID:"DockerCred",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubuser")])
                // sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                }   
            }
        stage('Deploy') {
            steps {
                echo 'Deploy Stage'
                // sh "docker run -d -p 8000:8000 prashw23/notesapp2:latest"
                sh "docker-compose down && docker-compose up -d"
                }   
            }
        }
    }


