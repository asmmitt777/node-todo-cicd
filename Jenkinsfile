pipeline {
    agent any

    stages {
        stage('code') {
            steps {
                git url: 'https://github.com/asmmitt777/node-todo-cicd.git', branch: 'master'
            }
        }
        stage('build and test') {
            steps {
                sh 'docker build . -t docker9asmit/node-todo-cicd:latest'
        }
      }
        stage('login and push'){
            steps{
                withCredentials([usernamePassword(credentialsId:'dockerHub',passwordVariable:'dockerHubPassword', usernameVariable:'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push docker9asmit/node-todo-cicd:latest"
            }
          }
        }
        stage('deploy'){
            steps{
               sh 'docker-compose down && docker-compose build --force-rm --no-cache && docker-compose up -d'
            }
        }
      
   }
}
