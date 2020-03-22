![Docker PROD Image CI](https://github.com/felixlapalma/pysteps-docker/workflows/Docker%20PROD%20Image%20CI/badge.svg)

# pysteps-docker

Repo to leave dockerfiles for pySTEPS lib

## Requirements

- docker

## Docker build

### Docker dev env

Build docker using [Dockerfile](dev/Dockerfile) provided,

	> docker build -t pysteps_dev -f dev/Dockerfile .

Base conda env is updated during build with  [environment_dev.yml](https://raw.githubusercontent.com/pySTEPS/pysteps/master/environment_dev.yml), so at
docker run, conda base env has all the libraries (no need to activate any env)
This image will install pySTEPS from master branch of [pySTEPS](https://github.com/pySTEPS/pysteps).
If you have forked the repo, just replace at built time ARG gitUser:

	> docker build --build-arg gitUser=_YOUR_USERNAME_ -t pysteps_dev -f dev/Dockerfile .

pySTEPS lib is installed at /opt/src dir from docker and additionally /opt/data is created for 
data io.

### Docker prod env

Build docker using [Dockerfile](prod/Dockerfile) provided,

	> docker build -t pysteps_prod -f prod/Dockerfile .

Base conda env has all the libraries (no need to activate any env). Additionally /opt/data is created for 
data io.

## Docker run

Now we can run a console in the the Docker container by doing

    	> docker run --rm -it 
    	-v _local_data_dir:/opt/data \
     	pysteps_{dev/prod} /bin/bash
