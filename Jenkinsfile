pipeline {
agent any
environment {
    DOCKER_IMAGE = "rajeshtutta123/game_warrior"
}

stages {

    stage('Clone Repo') {
        steps {
            git branch: 'main', url: 'https://github.com/rajeshtutta/Game_warrior.git'
        }
    }

    stage('Build Docker Image') {
        steps {
            sh 'docker build -t $DOCKER_IMAGE:latest .'
        }
    }

    stage('Push Docker Image') {
        steps {
            withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                sh 'echo $PASS | docker login -u $USER --password-stdin'
                sh 'docker push $DOCKER_IMAGE:latest'
                sh 'docker logout'
            }
        }
    }

}

}
