pipeline {

  agent any

  environment {
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
              docker build -t $DOCKER_REPOSITORY/$IMAGE_CAST:$DOCKER_TAG cast-service
            '''
          }
        }
        stage('movie') {
          steps {
            sh '''
              docker rm -f $IMAGE_MOVIE
              docker build -t $DOCKER_REPOSITORY/$IMAGE_MOVIE:$DOCKER_TAG movie-service
            '''
          }
        }
      }
    }

    //stage('run and test image') {
    //  steps {
    //    script {
    //      sh '''
    //        docker run -d -p 8002:8000 --name $IMAGE_MOVIE $DOCKER_REPOSITORY/$IMAGE_MOVIE:$DOCKER_TAG
    //        curl http://localhost:8001/api/v1/movies
    //      '''
    //    }
    //  }
    //}
  }
}
