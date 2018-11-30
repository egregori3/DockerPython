# DockerPython
Instructions for using Docker as a virtual environment for Python.

## Docker Cheat Sheet

https://github.com/wsargent/docker-cheat-sheet

## Docker Image

https://hub.docker.com/r/conda/miniconda3/

## Using the Docker Image as a Virtual Envirionment

### On Host

Execute in directory containing Python source.

```
docker pull conda/miniconda3
docker run -it --name <virtual env name> -v "$(pwd)"/:/app conda/miniconda3

To restart the last venv exited
docker start -a -i `docker ps -q -l`

To see processes venv in container
docker container top <virtual env name>

To see stream of stats
docker container stats <virtual env name>

To remove all stopped venv
docker container prune

To remove a stopped venv
docker container rm <virtual env name>
```

### In Container

The Python source directory will appear in the container /app directory.
You can edit the Python source usind an editor in the host (Sublime is the best).
You must execute the python code in the container (virtual image).

To install packages, run PIP in the container.

### Examples

```
eric@ubuntu:~$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
62a4b68ba065        conda/miniconda3    "bash"              24 seconds ago      Up 22 seconds                           grading
```

```
eric@ubuntu:~/Desktop/KBAI-Syllabus-Chatbot/Fall2018/TAeyesOnly/Project1$ ls
AgentGrader.py  AgentInterface.py  common.py  README.md  StudentAgent.py  TestQuestions.json

eric@ubuntu:~/Desktop/KBAI-Syllabus-Chatbot/Fall2018/TAeyesOnly/Project1$ docker run -it --name grading -v "$(pwd)"/:/app conda/miniconda3

root@62a4b68ba065:/# ls
app  bin  boot	dev  etc  home	lib  lib32  lib64  libx32  media  mnt  opt  proc  root	run  sbin  srv	sys  tmp  usr  var
root@62a4b68ba065:/# cd app
root@62a4b68ba065:/app# ls
AgentGrader.py	AgentInterface.py  README.md  StudentAgent.py  TestQuestions.json  common.py
root@62a4b68ba065:/app# 

```
