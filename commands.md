Steps 1 to 3 are for setting up VM

First lets update our system
4. Run command: sudo apt-get update

5. Install Docker on VM
Run command: sudo apt-get install docker.io

6. Check the docker version
Run command: sudo docker --version


7. Check if Docker is running
Run command: sudo systemctl status docker

8. Create a new user called docker-user with dummny password 1234
Run command: sudo adduser docker-user

9.  Grand sudo access to new docker-user
Run command: sudo usermod -aG sudo docker-user

10. Provide user with docker sudo, allows you to run docker commands without always specifying sudo
Run command:  sudo usermod -aG docker docker-user

11. Switch to new user
Run command: su - docker-user

12.  Test to see if everythihng is working
Run command: docker


13. Run the test 
Run command: docker run hello-world

14. Search for images
15.  Pull image
Run command: docker pull ubuntu

16. Check what images you have
Run command: docker images

17. Show all the running containers
Run command: docker ps -all

18. Delete the container, get container id from previous comman
Run command: docker rm 1696818bcb38

20. Create a new container using Ubuntu image
NB: the -it is for interactive. It will open inside the container 
Run command: docker run -it --name mini-ubuntu ubuntu

21. Exit the container
Run command: exit

22. If we want to list only the running containers, we can try the following command.
$ docker ps -all

Shorthand	Description
--all, -a	Show all containers (default shows just running)
--latest, -l	Show the latest created container (includes all states)
--size, -s	Display total file sizes
--filter, -f	Filter output based on conditions provided

25. Start the container again
Run command: docker start mini-ubuntu

26. Attach(connect) to running container shell
Run command: docker exec -it mini-ubuntu /bin/bash

NOTE: The # symbol means you are in container while the $ means you are in virtual machine

27. You can exit the container without stoping the container by entering
Control + C, and then Control + D
This will take you back to the vm

28. Check to see what containers are running
Run command: docker ps -all or docker ps -a

29. You can stop the container
Run command: docker stop mini-ubuntu


30. Finally lests rmove the container
Run command: docker rm mini-ubuntu

31.  Lets try create a python container
Run command: docker search python

32. We will use this to create a new python container
Run command: docker run --name mini-python-container -it python

This will pull down the image and start the cotiner.  Because of the -it param it will start in
interactive shell on the container

36. Run and save a command on your vm
Run command: echo "print('Hello World')" > test.py

37. check if file is and see what it looks like there
Run command: ls
Run command: cat test.py

38. Copy the file from vm inside the new container
Run command: docker cp test.py mini-python-container:/home

39. Lets try execute file
Run command: docker exec -it mini-python-container python /home/test.py


40. Now lets orgainise our commands; instead of running all these manual tasks, lets create a docker file
which is a set of commands/steps
* create a new file
Run command: pico Dockerfile

* paste below
FROM ubuntu:latest
RUN apt-get update -y
RUN apt-get install software-properties-common -y
RUN apt-get install python3.10 -y
ADD . /app
WORKDIR /app
CMD ["python3", "test.py"]


* Build the image, we will call it mini-python3-image
Run command: docker build -f Dockerfile . -t mini-python3-image


41. Run the container
Run command:


42. Stop and Remove the container
