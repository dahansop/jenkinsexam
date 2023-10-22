pipeline {

  agent any

  environment {
    DOCKER_ROOT_REPOSITORY = "dahansop"
    DOCKER_REPOSITORY = "dahansop/jenkinsexam"
    DOCKER_TAG = "V${BUILD_ID}.0"
    IMAGE_MOVIE = "movie"
    IMAGE_CAST = "cast"
  }

  stages {
    stage('build image') {
      parallel {
        stage('cast') {
          steps {
            sh '''
              docker rm -f $IMAGE_CAST
              docker build -t $DOCKER_REPOSITORY-$IMAGE_CAST:$DOCKER_TAG cast-service
            '''
          }
        }
        stage('movie') {
          steps {
            sh '''
              docker rm -f $IMAGE_MOVIE
              docker build -t $DOCKER_REPOSITORY-$IMAGE_MOVIE:$DOCKER_TAG movie-service
            '''
          }
        }
      }
    }

    stage('push image') {
      environment {
        DOCKER_PASS = credentials("DOCKER_HUB_PASS")
      }
      steps {
        script {
          sh '''
            echo $DOCKER_PASS | docker login --username $DOCKER_ROOT_REPOSITORY --password-stdin
            docker push $DOCKER_REPOSITORY-$IMAGE_CAST:$DOCKER_TAG
            docker push $DOCKER_REPOSITORY-$IMAGE_MOVIE:$DOCKER_TAG
          '''
        }
      }
    }


  }
}
