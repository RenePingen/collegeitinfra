# Introduction
This repository contains lab examples for IT infrastructure lectures on virtualization and cloud. The content will be handled in more detail in the lectures. This manual consist of two parts: reading material and hands-on lab. The reading material and labs help in understanding the concepts of virtualization and container technology.

## Reading material
Read through the following pages to get an understanding of virtualisation and container technology:
https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b/
https://www.freecodecamp.org/news/docker-simplified-96639a35ff36/ ( this second link already contains some practical examples)

## Lab excercises
Based on the instructions in the second link you can choose to use play-with-docker (https://labs.play-with-docker.com/) or install docker on your own computer.

The instructions below are based on play-with-docker. Also watch the video in this repository for an explanation.

### 1. Launch the docker helloworld application

Use the docker console/terminal (the screen in which you can control docker) to execute the following docker command:
```docker run hello-world```

Expected result:
```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```
### 2. Start a webserver in a docker container
In this excercise you will start a webserver in a docker container that can be accessed through a browser. 
Run the following docker command:
```docker run -d -p 80:80 --name webserver1 nginx```

Check if the container is running:
```docker ps```
Expected result:
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                NAMES
ea5a87732acf        nginx               "nginx -g 'daemon of…"   5 seconds ago       Up 3 seconds        0.0.0.0:80->80/tcp   webserver1
```

Check if you can access the application through the browser. In play-with-docker, you can do this by clicking on the port number on the top of the screen (port 80 in this case).

Kill the container
``` docker kill webserver1```

### 3. Start your own web application in docker
In this excercise you will start a custom web application.

Download the code for the web application by cloning the git repository. Execute the following command in the console/terminal:
```git clone https://github.com/RenePingen/collegeitinfra.git ```

#### Optional: make a change in the webpage
Use the editor to change the file index.html in the folder collegeitinfra/Webserverdemo. In the docker web environment (play-with-docker), click on "Editor", navigate to the right folder and file index.html, and edit and save the changes.

#### Build the docker image
Build the docker image by running the following command. This will tell docker to take the docker file, index.html and create a docker image out of it that we can launch.
```docker build -t webserverdemo collegeitinfra/Webserverdemo/```

#### Launch the custom docker container
Launch the custom docker container by running the following command:
```docker run -d -p 81:80 webserverdemo```

### Test the container
Check if you can access the application through the browser. In play-with-docker, you can do this by clicking on the port number on the top of the screen (port 81 in this case).

#### Launch a second container
To show the power of docker, now launch a second container with the same image. We need to use a different port on the host machine, so:
```docker run -d -p 82:80 webserverdemo```

Check if you can access the application through the browser. In play-with-docker, you can do this by clicking on the port number on the top of the screen (port 82 in this case).

####Optional 4. Launch a virtual desktop with a web interface
To show the power of virtualisation we will run a virtual desktop in a docker container. For this we will use a docker image which has a full version of Linux with user interface and remote access possibilities (through VNC).

Run the following command in docker:
``` docker run -d -p 5901:5901 -p 6901:6901 consol/centos-xfce-vnc ```

Check if you can access the application through the browser. In play-with-docker, you can do this by clicking on the port number on the top of the screen (port 6901 in this case). Use the password "vncpassword" to access the desktop.







