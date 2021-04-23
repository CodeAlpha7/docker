# docker
Contains step-by-step procedure to create Dockerfile, custom images and deploy containers to behave as virtual hosts

-----TUTORIAL ON HOW TO USE DOCKER-----

step-1: create a new Dockerfile
	
	$ mkdir -p nginx-image;  	//create fresh directory
	$ cd nginx-image/  		//open the location
	$ touch Dockerfile		//creates new Dockerfile 
	
	$ vim Dockerfile		//opens it using vim editor
	

step-2:initialize an image 

	you can copy a base image and make changes to it as required
	
	$ FROM ubuntu:trusty		//copies base image
	
	$ RUN apt-get update && apt-get install -y iperf3
	$ RUN apt-get install -y tcpdump && mv /usr/sbin/tcpdump 		/usr/bin/tcpdump
	$ RUN apt-get install -y hping3
	

step-3: create image by building it

	$ sudo docker build -t endpoint:latest
	
	//this creates an image named "endpoint" using Dockerfile
	//navigate to the directory where Dockerfile is located before 		executing this command

step-4: create containers for that image

	$ sudo docker run -d --privileged --name=int --net=none 
	endpoint:latest tail -f /dev/null
	
	//creates docker container named "int" which is your host
	//disable default (docker) networking using "--net=none"
	//container should run with "priveleged" flag 
	//"-d" flag makes the container run as a daemon
	//container needs to be alive for the duration of the experiment
	so make it do something useless like monitoring the contents of
	an empty file keeping it alive forever