# Docker-voting-app-example
This is based on the Bret Fisher's Udemy course https://www.udemy.com/course/docker-mastery/

Check his Docker Hub repo: https://hub.docker.com/u/bretfisher

The images listed in the Docker stack file are found in my private repo so these won't work for you except the image: bretfisher/examplevotingapp_worker:java

You may replace the images as it follows:

  redis_service:
    image: redis:alpine

  database_service:
    image: postgres:9.4
 
  vote_service:
    image: bretfisher/examplevotingapp_vote

#already replaced in the stack
  result_service:
    image: bretfisher/examplevotingapp_result

  worker_service:
    image: bretfisher/examplevotingapp_worker:java

  visualizer_service:
    image: dockersamples/visualizer
