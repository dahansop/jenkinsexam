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
      steps {
        script {
          sh '''
            docker rm -f $IMAGE_MOVIE
            docker build -t $DOCKER_REPOSITORY/$IMAGE_MOVIE:$DOCKER_TAG movie-service
          '''
        }
      }
    }

    stage('run and test image') {
      steps {
        script {
          sh '''
            docker run -d -p 8001:8000 --name $IMAGE_MOVIE $DOCKER_REPOSITORY/$IMAGE_MOVIE:$DOCKER_TAG
            curl http://localhost:8001/api/v1/movies
          '''
        }
      }
    }
  }
}
