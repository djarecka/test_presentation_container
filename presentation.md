name: inverse
layout: true
class: center, middle, inverse
---
# Using reproducible container based environments
---
layout: false
### Why do we need containers?

- Science Reproducibility

--

    - Each project in a lab depends on complex software environments
        - operating system
        - drivers
        - software dependencies: Python/MATLAB/R + libraries
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
$ docker pull busybox
$ docker images
$ docker run busybox
$ docker run busybox echo ``hello from busybox''
$ docker run -it busybox sh
$ docker ps
$ docker rm
$ docker run -it --rm busybox
$ docker run -it --rm -v YourDirectory:/src busybox
```

---
### Docker: Installing software with Dockerfile

- Dockerfile content:

```bash
# TODO: update image (Satra)
FROM bids/base_fsl
RUN apt-get update -y && apt-get install -y r-base
```

--

- Building a new container:

```bash
$ docker build -t fslR .
```

--

- Running your new container:

```bash
$ docker run -ti --rm fslR
```

---
### Docker and Nipype

- Using Nipype official Docker image

```bash
$ docker images
$ docker pull nipype/nipype
$ docker run -it --rm nipype/nipype
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
