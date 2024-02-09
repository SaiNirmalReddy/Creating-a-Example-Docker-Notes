
Introduction to Containers

------------------------------------------------------------------------------------------------------------------------------------------------
-
-> Container use the concept of Docker and Docker containers are very light weight because they have the minimal operating system(base operating sysyem) that means they have a base image and whenever they require dependencies , they will take them from the base operating system

-> Dockers are package of Application libraries and system dependencies and for example if one vm is running on linux and if other needs other o.s., docker will take the help of base operating system .

-> Docker basically runs on a bare metal or a physical srver on a virtual machine , and it consumes the resources from the host operating system other than the minimalistic dependencies that it has inside the container and it has the source code and system dependencies in itself but if an application requires some information like it has to consume something from the kernel and if it has to do some system calls, only that things it will do from the host operating system . 

-> Dockers containers are easy to ship from one place to other place that means it can ship from one place and deploy on kubernetes cluster .

-> To contaneraize any application, we need to first write a Docker file . 

-> Docker Life Cycle 
-->Docker File ->(Execute the file and convert in to Docker Image) Docker Image ->(and convert this docker image to) Docker Container 

-> Docker have the Docker Engine where files and images will be submitted to it . 

-> Dockers have disadvantage because it depends on Docker Engine and for suppose this Docker Engine gets down , We lost the containers and Images , so to get this right we have the concept and tool called "Buildah"  which will takes the responsibility of Docker containers by writing commands in shell scripting and that will create a Docker Image. 

-> Buildah tool will solve the Single Point Of Failure problem and Docker Layers problem and it works well with scopio and podman .  


Real time Work - 

1) CLI - EC2 AWS - Dev - Git - sourcecode - clone -  container code in Docker - for example - error - rereturn - Dev - Once back - Code - container code and scripts - Jenkins - Orch - Kubernetes Cluster 

Application - Java Application code - www.facebook.com - Java+DB -> Buildtools - Like Maven, Sonar , Gradl 

Generation of .war, .rar files - Docker script

- > In Real Time - we need approvals for Git, Jenkins and even to folders 


Interview - CI/CD - CD - 2 types , Diff b/w Continuous Development and Continuous Delivery 

-> Continuous Development - 
-> Continuous Delivery  - 





--------------------------------------------------------------------------------------------------------------------------------------------------

# Creating-a-Example-Docker-Notes
This is a Notes of Creating a Example Docker 


CONTAINERS (DEVOPS)
 


-> As a Devops Engineer, to contaneraize any application, we need to first write a Docker file . 

 1 - Choose a base Image like Ubuntu or CentOS 

    -> FROM ubuntu

 2 - From Ubuntu , I choose a WORKDIR 

WORKDIR - It is basically a identification on where your source code is going to save (or) Let's say your organization have multiple projects and whenever you are writing a DOCKER FILE, you can create  a standard saying that we will always put the source code whenever we are containeraing the application in a folder called slash app (/app) . 

   ->  WORKDIR /app

 3 - Afterthat, copy the requirements.txt file to the /app file (Inside your work directory) 

   ->  COPY requirements.txt /app
   ->  COPY devops /app (As in Source Code)

 Because,  requirements.txt is the file where you have dependencies for example if you use python, U will have the python dependencies of the Django application and TZ data .  

 4 - Afterthat, we copy the source code to the WORKDIR (/app) , beacuse using the source code and dependencies you will form a bundle or you will form the binary of your application .
  
    ->  COPY devops /app (As in Source Code)

 5 - Later you write the RUN and installation packages of the specific application or framework ,
For example , for Django , We install Python packages and dependencies . 

  RUN apt-get update && \
  apt-get install -y python3 python3.pip && \
  pip install -r requirements.txt && \
  cd devops

 6 - And the final command , we should know as a Devops Engineer about "ENTRPOINT" and "CMD"

 7 - "ENTRYPOINT" and "CMD" execute your start command or whenever someone runs your Docker command, both "ENTRYPOINT" and "CMD" can serve as your starting point but the only difference is "ENTRY POINT" is something which you cannot change and whenever you are running the container, Let's say if I define "PYTHON3" - they can "OVERRIDE" this value in your Docker Image and whereas "CMD" is something that is configuarable) 

-> ENTRYPOINT ["python3"] - main executable on the ENTRYPOINT
-> CMD["manage.py", "runserver", "0.0.0.0:8000"] - is modifiable according to the application requirements and the ports you alloted . 

------------------------------------------------------------------------------------------------------------------------------------------------



Day 26

 MULTI STAGE DOCKER BUILDS


-> The concept has been come into picture beacause , day 2 day we are wasting lot of VM'S data so get this right we will start with Mutli stage Docker build, where in stages Docker containers are build and for example in 1st stage, we use the base OS from UBUNTU, but in final stage we just use only the environments which are required to run the application .

-> The advantage of this concept is higly secured because we don't use any commands or shell scrpting in this Multi stage docker builds . 

-> There is another concept which is "DISTROLESS IMAGES" which means we will reduvce the image size to as small as possible that means the image size is reduced to the lower extent because we just use the run time environments and wherein we use the concept of Multi stage Docker images . 

->  If you are using applications like Golang , this is secured .

 
------------------------------------------------------------------------------------------------------------------------------------------------


Day 27 

DOCKER BIND AMOUNTS AND VOLUMES

-> Let's say we have a CONTAINER and we have installed an "NGINX" application inside this CONTAINER , and what's this application does isk keeps the data of login user and time slots in the "LOGFILE" . (for example for last 5 days,10days) .  

-> This concept has come into picture because "CONTAINERS" have drawbacks like if for suppose , container goes down due to some issues , the "LOGFILE" will be deleted because we don't have file system for CONTAINER  because they are very light weight in nature , they usually do is they just resources like use kernel and resources from host operating system and these resources and not permanent resources of the container . 


-> So now if the "LOGFILE" is deleted, the information of the users logins and authentication of users are deleted .

  -> Problem 1 - We don't have Previous Logfiles for auditing  


-> For example , we have front end and back end containers, and now back end container keeps on writing a file and now this file has to be read by the front container to display the contents like BACKEND container write the JSON files or YAML files and for some reasons BACKEND CONTAINER goes down , then front end can only serve the files which are latest records but not the previous records .

   -> Problem 2 - Cannot read all data from both the FRONT and BACK END


- Another example, we have a CONTAINER and it reads a file that is provided from a CRONJOB on the host and  "CRONJOB" is periodical job which is running on the host and it create a file on the host like "JSON" or "YAML" file and but there is no standard way till now that CONTAINER can take a SPECIFILE DIRECTORY OR a SPECIFILE FILE from the operating system . 

   -> Problem 3 - It can use resources and but don't know how to read files from SPECIFILE DIRECTORY OR a SPECIFILE FILE SYSTEM.

So, TO SOLBVE THIS PROBLEM , DOCKER CAME WITH TWO CONCEPTS 

1. BIND MOUNTS 

2. VOLUMES 


 ->  BIND MOUNTS does is binds the SPECIFIC DIRECTORY on the HOST to a SPECIFIC DIRECTORY on the CONTAINER . 


 -> For example we have a CONTAINER C1 have a folder and have a folder in HOST OS, Let's say we have folder called "/app"  in both the container and host , so by using the concept of "BIND MOUNTS" , we will be having the data present in both CONTAINER AND HOST .


 -> DOCKER  VOLUMES  

 -> VOLUMES have a LIFECYCLE 

 -> Using a DOCKER CLI and DOCKER COMMANDS , we can create a volumes and  
     VOLUME is something you are a LOGICAL PARTITION on the HOST and you         can manage the things like CREATE a VOLUME , DESTROY a VOLUME .

   -> We can attach VOLUMES to multiples CONTAINERS like C1,C2 ,Technically both are solving same problem , Even using the VOLUME,we are attaching a SPECIFIC DIRECTORY to the "CONTAINER"  but the main advantage is using VOLUME we are not providing DIRECTORY details like  
we are nor "/app" folder on the host should be assigned to specific folder on the "CONTAINER" instead you are saying CREATE a VOLUME on the HOST aand this VOLUME is basically a LOGICAL PARTITION on the HOST . 


   -> Whereas in the "BIND MOUNTS" Let's say you are using a CONTAINER and if you are trying to bind a one specific DIRECTORY to another DIRECTORY on the host , then you are only restricted on that specific HOST , Whereas by using "VOLUMES" , we can CREATE VOLUME on any place like on same HOST or any external "EC2 INSTANCE" these are known for external sources where we have the "BACK-UP" of the data and in later point of time , we can easily from cloud provider to local storage anything like you can play around VOLUMES . 

   -> Whenever youa re trying to mount a VOLUME to the CONTAINER , you use         
"docker -v <args> 

   -> docker --mount is more verbose , you elaborate the details like "src", "destination" , "permissions" in the container . 


   -> Whenever you are trying to mount a VOLUME to the CONTAINER , you use         
"docker -v <args> 

   -> docker --mount is more verbose , you elaborate the details like "src", "destination" , "permissions" in the container . 


   ------------------------------------------------------------------------------------------------------------------------------------------------


 DOCKER COMMANDS



50 Docker Commands For Container 
Management, Image Manipulation, . 
. Networking & More
Container Management:
1. Run a Container:
docker run [OPTIONS] IMAGE[:TAG] [COMMAND] [ARG...]
2. List Running Containers:
docker ps
3. List All Containers:
docker ps -a
4. Stop a Running Container:
docker stop CONTAINER_ID
5. Remove a Container:
docker rm CONTAINER_ID
6. Remove All Stopped Containers:
docker container prune
7. Inspect Container Details:
docker inspect CONTAINER_ID
8. Attach to a Running Container:
docker exec -it CONTAINER_ID /bin/bash
Image Manipulation:
9. List Local Images:
docker images
10. Pull an Image from Docker Hub:
docker pull IMAGE[:TAG]
11. Build an Image from Dockerfile:
docker build -t IMAGE_NAME:TAG PATH_TO_DOCKERFILE
12. Remove an Image:
docker rmi IMAGE_ID
13. Remove All Unused Images:
docker image prune
Networking:
14. List Networks:
docker network ls
15. Inspect Network Details:
docker network inspect NETWORK_ID
16. Create a Bridge Network:
docker network create --driver bridge NETWORK_NAME
17. Connect Container to Network:
docker network connect NETWORK_NAME CONTAINER_NAME
18. Disconnect Container from Network:
docker network disconnect NETWORK_NAME CONTAINER_NAME
Volume Management:
19. List Volumes:
docker volume ls
20. Inspect Volume Details:
docker volume inspect VOLUME_NAME
21. Create a Volume:
docker volume create VOLUME_NAME
22. Remove a Volume:
docker volume rm VOLUME_NAME
Container Logs:
23. View Container Logs:
docker logs CONTAINER_ID
24. Tail Container Logs:
docker logs -f CONTAINER_ID
Docker Compose:
25. Run Docker Compose:
docker-compose up -d
26. Stop Docker Compose Services:
docker-compose down
27. Build and Run Docker Compose:
docker-compose up --build -d
Docker System:
28. Display System-Wide Information:
docker info
29. Show Docker Disk Usage:
docker system df
30. Remove All Unused Data:
docker system prune
Docker Registry:
31. Login to Docker Hub:
docker login
32. Push Image to Docker Hub:
docker push IMAGE[:TAG]
33. Pull Image from Private Registry:
docker pull REGISTRY_URL/IMAGE[:TAG]
Docker Swarm:
34. Initialize Docker Swarm:
docker swarm init
35. Join Node to Swarm:
docker swarm join --token TOKEN IP:PORT
36. List Nodes in Swarm:
docker node ls
37. Create a Service:
docker service create [OPTIONS] IMAGE[:TAG] [COMMAND] [ARG...]
38. Scale a Service:
docker service scale SERVICE_NAME=REPLICAS
39. Inspect Service Details:
docker service inspect SERVICE_NAME
40. Remove a Service:
docker service rm SERVICE_NAME
Docker Security:
41. Check Container Vulnerabilities:
docker scan IMAGE[:TAG]
42. Run Container with Security Options:
docker run --security-opt seccomp=unconfined --cap-add=SYS_PTRACE -it 
IMAGE[:TAG]
43. Run Container with Readonly Filesystem:
docker run --read-only -it IMAGE[:TAG]
Docker Stats:
44. Display Real-time Container Resource Usage:
docker stats CONTAINER_ID
Docker Events:
45. Monitor Docker Events:
docker events
Docker Debugging:
46. Inspect Docker Bridge Network:
docker network inspect bridge
47. View Docker Daemon Logs:
journalctl -u docker
48. Check Docker Version:
docker version
Miscellaneous:
49. Copy Files between Host and Container:
docker cp SOURCE_PATH CONTAINER_ID:DEST_PATH
50. Create a Custom Docker Bridge Network:
docker network create --driver bridge --subnet=SUBNET_NAME 
CUSTOM_NETWORK_NAME
This cheat sheet covers a wide range of Docker commands for container 
management, image manipulation, networking, and more. Customize commands 
based on your specific use case and requirements.

docker exec -it login /bin/bash


   -> docker build -t tagname

   -> docker run -it(interactive mode) -p(port) -d(detach mode) <image> 

   -> docker ps -a [list of running containers]

   -> docker head -5
   
   -> docker ps -a | grep NAME

   -> docker images

   -> docker volume create name

   -> docker volume rm "NAME"

   -> docker inspect followed by "Name of the Container"

   -> docker run -d --mount source=name of the volume, target= "/app" (target on the container like /app) and followd by <IMAGE> image details 

   -> To stop any VOLUME , fisrt we need to stop CONTAINER 



Doubt : not getting the image reduced in multi stage 

Doubt : not getting the output of vloumes 



Day 28

 DOCKER NETWORKING

 -> Basically, Networking allows containers to communicate with each other and host system .

 
 -> For Example, On a EC2 INSTANCE/HOST , A Docker is installed and we have two containers Front end C1 and Front end C2 and they have to communicate with each other using the concept of NETWORKING (IP address) 


  COMPARING DOCKER NETWORKING WITH VM NETWORKING


  -> Let's say each VM has its own Operating system and applications and each application is completely isolated from each other and they both have differnt IP'S and different subnetmasks.  
 

 -> For example, we have two containers like C1 has just a Login Info and C2 has Payment Info which is a secured information and anybody who has access to Login Container shouldn't have access to payment container, Container Networking offers the solution .


  HOW A CONTAINER TALKS TO HOST OPERATING SYSTEM 

   1) C1 <-> C2 

   2) C1 has isolation to C2 



   -> If C1 has to talk to Host and Host has the bydefault ethernet with some IP , What Docketr Networking has done is there should be a medium and that medium is "virtual ethernet" and by default docker has it and this is known as Bridge Networking and this "Bridge is DOCKER 0 with virtual ethernet" . 

 
   

   We have lot of ways that containers can commincate with each other
  

   1) Bridge Networking 

   2) Host Networking -> Secure 

   3) Overlay Networking -> Kubernetes , Swarm 

   -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

 
   " Scenario 2 "

  If C1(Payment) has to be isolated from C2(LogIn) , then the Docker uses the concept of "CUSTOM BRIDGE" and by that C2 can talk with the Host , it means to secure the C1(payment) Container, we should create a "CUSTOM BRIDGE" by using Docker Network command .  



Doubt - unable to install ping and why we are using two different CLI's , and if have 100's of containers and logins.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

                                                                          Day-29


                                                                 DOCKER INTERVIEW QUESTIONS


1) -> What is Docker ?

Ans: Docker is basically a containerization platform which is used to build containers and to manage the lifecycle of the containers . 


In Interviews , You should say as I use docker to basically build the docker images, docker files, run containers and push them to registeries .
 

2) How Containers are different from Virtual Machines ? 

 Ans: Containers are very light weight in nature because they don't have the complete operating system . Whereas in Containers, you install Docker platform and we are creating containers and whereas in VM'S , we install Hypervisor on top of it we have VM'S but in VM's we have the complete guest operating system so that image size will be very high and when yoy talk about CONTAINER , ypu basically have application and system dependencies and some system libraries and containers use other resources from host operating system . 

Ex: Java -> JRE and dependencies ->  Containers 

  Java -> Ubuntu Os, Kernel and system libraries - Virtual Machines


3) What is Docker Life Cycle?

Ans: Right from the stage of writing Docker file -> building a Docker Image -> to creating a Docker Container and pushing them to the registry .

 ->Example :  Let' say a development team has approached and the requirement is to containeraize an application, we intially start with writing a "Docker file", I will write the Docker file with set of instructions and once I feel that the "Docketr file" is complete I will create a "Image" out of it by using the "DOCKER CLI" and run the commands loke Docker build to convert the file to image and docker run to execute the container and finally we push the "IMAGES" to external registeries like "DOCKER HUB" or ECR . 


4) What are the components in Docker?

 Ans:  When you Install the Docker , we get the components like Client in which we use commands like (docker build , docker pull, docker run) , Docker HOST where we have the "Docker deamon"(which is responsible for executing your actions) and the Containers and Images and next Docker Registry (where we have the external registeries like docker hub and nginx)  


-> Example : Let's say , you are executing a command called docker build and submit it to Docker CLI and that request actions are received by "Docker deamon"(every action will be received bu docker deamon) which is heart of Docker and will try to take this and execute the actions and push them to docker registry and create a specifc Image . 


5) What is the difference between docker COPY and docker ADD ? 

 Ans: Docker ADD command can copy the files from a URL while Docker COPY command can copy files from host system into the container .

 Example : Let's say you want a "logfile" from the AWS S3 STORAGE or any RAW file from Git hub , you can use Docker ADD command .

Example : Let's say ypu want to copy a "source code" from your file system or EC2 Instance , you use Docker COPY command . 



6) What is the difference between CMD and Entrypoint in Docker ?

 Ans: CMD is basically let's say you want to pass from arguments to the container and this arguments can be overridden .

Example : CMD - Let's say you want to run a "Python" related function for the calculator function , then the arguments should be passed and overridden acc to the requirement . 

 "Host URL, Host ports should be written in CMD"
 

 Entrypoint :  In "Entrypoint" , parameters shouldn't be overridden by default should be pass in Entrypoint . 

   "python , manage.py" -> ENTRYPOINT


7) What are the networking types in Docker and what is the default ?

 Ans:  1) Bridge Network (default) - Bridge network is a medium which has a virtual ethernet (veth) or docker 0 network -> using which a container can access your host network . 

   2) Overlay - When we have multiple Hosts and when we use docker swarms and kubernetes it will come into picture . 
       
       3) Host - By using Host network, you will bind the host n/w with the container n/w and there is no virtual ethernet.

       4) MacVlan - MacVlan will allows the container to appear on the network as a physical host rather than a container . 


8)  Can you explain how to isolate networking between the containers ? 

Ans: "To isolate the networking between the containers , we us the concept of "CUSTOM BRIDGE" network by which we secure the networking b/w the containers and the command we use is

"docker -d --name --network=secure-network" by which this container is secured and cannot talk to other container . 


9) what is a multi stage build in Docker ? 

Ans:  The Multi stage docker build has come into picture to reduce the Image size as much as possible and while in the Dockerfile and we copy the application binaries and artifacts which don't have any ubuntu or run time dependencies from first stage to final stage and the major advantage of this is to build light weight containers . 

-> In the first stage we install all dependencies and the once the application is bulid, all these dependencies are not required and what you do is in final stage we can simply the copy of binaries or the executables that we have created so that image size will be reduced as much as possible . 

 Example : Let's say you have a multi-tier apllication like front-end(python dependecies), back end(java depencencies) and db(connectors) and the final image will be jar file or winrar file so we just copy the JRE's binaries and we execute them in final stage si the RAR file image will be completely reduced . 



10) What are Distro less images in Docker ? 

Ans: Distroless images contain only your application and its runtime dependencies with a very minimum operating system libraries. They do not contain package managers , shells or any other programs you would expect to find a standard Linux distribution. They are very small and lightweight images  .

The advantage is your application is less exposed and highly secured .


Example : scrath is a distroless image . 



11) Real Time Challenges with Docker ?


Ans: -> Docker is a single deamon process. Which can cause a single point of failure, If the Docker Deamon goes down for some reason all the applications are down . 
-> To address this issue -  Tools like BUildah , Podman will address this solution beacuse Podman also have same docker instructions which address the docker issues and use same commands like docker . 

-> Docker Deamon runs a root user. Which is security threat. Any process running as a root can have adverse effects. When it is compromised for security reasons, it can impact other applications or containers on the host . - To address this issue , Podman will address it because it don't have the root user . 

-> Resource Constraints : If you're running too many containers on a single host, you may experience with resource constraints (for example if C1 used lost of memory or resources then C2 may don't have enough resources). This can result in slow performance or crashes . 

 To address this issue , we have to configure the resoures very well for the containers .


12)  What steps would you take to secure containers ?


Ans: 

VM'S have proper networking isolation becuase they have their own OS but whereas in Containers we don't have proper security becuase they don't have comple OS they just have the dependencies . So To resolve this issue 

Some of the steps,

  1) Use Distroless or Images with not too many packages as your final image in multi stage build, so that there os less chance of CVE or security issues.

2) Ensure that the networking is configured properly. This is one of the most common reasons for security issues. If required configure custom bridge network and assign them to isolate containers .

3) Use utilities like Sync to scan your container images . 

whenever you create container images in Jenkins pipeline, always try to use utilities like SYNC" and ensure that your images don't have any vulnerabilities , so youcan use the docker sync command to scan the container images before you push them to  production (or) staging environment . 















