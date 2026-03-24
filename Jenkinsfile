:pipeline {
agent any
environment {
  DOCKER_image = "rajeshtutta123/game_warrior"
}
stages {
  stage(clone repo) {
    steps {
      git branch: 'main', url: 'https://github.com/rajeshtutta/Game_warrior.git'
    }
  }
  stage(BUILD DOCKER IMAGE) {
    steps {
      sh 'docker build -t $DOCKER_image:latest .'
    }
  }
  stage(PUSH DOCKER IMAGE) {
    steps {
      withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
        sh 'echo $PASS | docker login -u $USER --password-stdin' 
        sh 'docker push $DOCKER_IMAGE:latest'
        sh 'docker logout' 
      }
    }
  }
}
