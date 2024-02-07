
Introduction to Containers

------------------------------------------------------------------------------------------------------------------------------------------------

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
