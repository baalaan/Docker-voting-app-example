**_This is a work in progress project_**

**Docker-voting-app-example**

This is based on the course [Bret Fisher's: Docker Mastery: with Kubernetes +Swarm from a Docker Captain](https://www.udemy.com/course/docker-mastery/)

**IMPORTANT NOTE**

The images listed in the docker stack file are found in my Docker Hub PRIVATE-REPO (for the moment it's PUBLIC but it's subject to lockdown at anytime!). 


**Replace the images for the following services**

If the images listed in the stack file are not accessible due to docker hub private repo lockdown then you may replace the images as it follows:

> redis_service:
>  image: redis:alpine

> database_service:
>  image: postgres:9.4
 
> vote_service:
>  image: bretfisher/examplevotingapp_vote

#already replaced in the stack
> result_service:
>  image: bretfisher/examplevotingapp_result

> worker_service:
>  image: bretfisher/examplevotingapp_worker:java

> visualizer_service:
>  image: dockersamples/visualizer


**Running the stack on a single Swarm node on your computer**

> docker swarm init

> docker stack deploy -c voting-app-example-stack-1.yml voteapp

**You should see the following getting created**

Creating network voteapp_default
Creating network voteapp_frontend
Creating network voteapp_backend
Creating service voteapp_redis_service
Creating service voteapp_database_service
Creating service voteapp_vote_service
Creating service voteapp_result_service
Creating service voteapp_worker_service
Creating service voteapp_visualizer_service

**Check to see if the services are running**

> docker stack services voteapp

You should see the following result (Check the REPLICAS column):
ID                  NAME                         MODE                REPLICAS            IMAGE                                           PORTS
eswua7z4rohq        voteapp_result_service       replicated          1/1                 stefandockerid/myprivaterepo:votingapp_result   *:5001->80/tcp
m2sv53ikwlss        voteapp_redis_service        replicated          1/1                 redis:alpine3.12                                *:30000->6379/tcp
my9pct0nsm3r        voteapp_worker_service       replicated          1/1                 bretfisher/examplevotingapp_worker:java
nlxc1fjvay2e        voteapp_vote_service         replicated          2/2                 stefandockerid/myprivaterepo:votingapp_vote     *:5000->80/tcp
rhyhoh2fxbvg        voteapp_visualizer_service   replicated          1/1                 dockersamples/visualizer:latest                 *:8080->8080/tcp
zmu9h48z6n7z        voteapp_database_service     replicated          1/1                 postgres:9.6

**Go to your browser of choice and access the following pages**

**Voting page**
http://localhost:5000

**Voting results page**
http://localhost:5001

**Visualizer page**
http://localhost:8080

