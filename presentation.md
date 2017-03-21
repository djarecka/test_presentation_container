name: inverse
layout: true
class: center, middle, inverse
---
# Using reproducible container based environments
---
layout: false
### Why do we need containers?

### <span style="color:#FAF5FF">Science Reproducibility</span>
--

  - Each project in a lab depends on complex software environments
    - operating system
    - drivers
    - software dependencies: Python/MATLAB/R + libraries
&nbsp;

--

  - We try to avoid
    - the computer I used was shut down a year ago, can’t rerun the results from my publication...
    - the analysis were run by my student, have no idea where and how...
    - etc.
---
### Why do we need containers?
--

- Collaboration with your colleagues
--

    - Sharing your code or using a repository might not be enough
--

- We try to avoid
  - well, I forgot to mention that you have to use Clang, gcc never worked for me...
  - don’t see any reason why it shouldn’t work on Windows...(I actually have no idea about Windows, but won’t say it...)
  - it works on my computer...
  - etc.
---
## Why do we need containers?

- Freedom to experiment!

--

<img src="img/universal_install_script_2x.png" width="40%" />
Universal Install Script from xkcd: The failures usually don’t hurt anything... Usually all your old programs work...
--

    - We try to avoid
        -I just want to Undo the last five hours of my life...
---
### Virtual Machines and Container Technologies

- Main idea: isolate the computing environment
    - Allow regenerating computing environments
    - Allow sharing your computing environments

--

- Two types:
    - Virtual Machines
        - Virtualbox
	- VMware
	- AWS, Google Compute, ...
    - Containers (?)
        - Docker
	- Singularity
--

- The details differ (and matter depending on application)

---
### Virtual Machines vs Container #TODO

<img src="img/Virtual_Machine_vs_Docker_Container.png" width="80%" />
---
### Virtual Machines vs Container #TODO

<img src="img/Virtual_Machine_vs_Docker_Container.png" width="80%" />
---
### Docker
- leading software container platform
- an open-source project
- bundle libraries and required settings only (not a full operating system)
- more lightweight to deploy and faster to start up than VM

--
- testing your Docker installation:
```bash
$ docker run hello-world
```
---

## Docker

- Using existing images
--

```bash
$ docker pull ubuntu
$ docker images
$ docker run ubuntu
$ docker run ubuntu echo ``hello from your container''
# running docker interactively
$ docker run -it ubuntu sh
# currently running containers
$ docker ps
# created containers
$ docker ps -a
# remove containers
$ docker rm <container_id>
# remove all stops containers
$ docker rm $(docker ps -a -q)
# --rm automatically remove the container when it exits
$ docker run -it --rm ubuntu
# add a data volume to a container (you can use multiple times to mount multiple data volumes)
$ docker run -it --rm -v YourDirectory:/src ubuntu
# read only mode
$ docker run -it --rm -v YourDirectory:/src:ro ubuntu
```
---
### Docker: Installing software with Dockerfile

- Create a new directory

```bash
$ mkdir mydockerbuild
$ cd mydockerbuild
```

- Dockerfile content:

```bash
FROM ubuntu:latest
RUN apt-get update -y && apt-get install git emacs
```

- Building a new container:

```bash
$ docker build -t my_new_container .
```

- Running your new container:

```bash
$ docker run -it --rm my_new_container
```

- Within container you can try:
```bash
$ git
$ emacs
```

--

- More about the Dockerfile syntax you can find [here](https://docs.docker.com/engine/reference/builder/#from)

- Example of Dockerfile to run Nipyp wokflow from [Docker Hub](https://hub.docker.com/r/miykael/nipype_level0/~/dockerfile/)
---
### Docker and Nipype

- Using Nipype official Docker image

```bash
$ docker images
# only if you haven't done it already
$ docker pull miykael/nipype_level3
$ docker run -it --rm miykael/nipype_level3
```

- Within the nipype container

```bash
python
```

- Within Python interpreter:

```python
import nipype
nipype.test()
```
---

## Docker

- Using Jupyter notebook with Docker container
TODO: sprawdzic,dlaczego nie moze byc 8880:8880 (to drugie musi byc 8888)
TODO sprawdzic opcje -d
```bash
$ docker run -it --rm -p 8880:8888 -v /home/vik/notebooks:/home/ds/notebooks(TODO) miykael/nipype_level3

```

--

---
### Singularity

- a container solution created for scientific and application driven workloads
- supports existing and traditional HPC resources
- a user inside a Singularity container is the same user as outside the container
- but you can use Vagrant to create a container (you have root privileges on your VM!)
- can run existing Docker containers
- [Satra's presentation](http://satra.cogitatum.org/om-images/}{Singularity on Openmind)
- [other tutorials](http://singularity.lbl.gov/tutorials)

---
name: inverse
layout: true
class: center, middle, inverse
---
# Questions?
