# Creating-a-Example-Docker-Notes
This is a Notes of Creating a Example Docker 


CONTAINERS (DEVOPS)


-> As a Devops Engineer to write a container will starts with 

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

 7 - "ENTRYPOINT" and "CMD" execute your start command or whenever someone runs your Docker command, both "ENTRYPOINT" and "CMD" can serve as your starting point but the only difference is "ENTRY POINT" is something which you cannot change and whenever you are running the container, Let's say if I define "PYTHON3" - they can OVERRIDE" this value in your Docker Image and whereas "CMD" is something that is configuarable) 

-> ENTRYPOINT ["python3"] - main executable on the ENTRYPOINT
-> CMD["manage.py", "runserver", "0.0.0.0:8000"] - is modifiable according to the application requirements and the ports you alloted . 
