FROM ubuntu:18.04

####### OS ###############################################
RUN apt-get update && apt-get upgrade -qy
RUN apt-get install -qy software-properties-common ca-certificates wget curl ssh
RUN apt-get install -qy build-essential
RUN apt-get install git -qy
####### OS ###############################################

############# MINICONDA install ##################################
#
RUN wget --quiet https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean --all -y && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

#update path
ENV PATH /opt/conda/bin:$PATH
#
############# MINICONDA install ##################################


############# pySTEPS_devenv ########################################
#
RUN wget https://raw.githubusercontent.com/pySTEPS/pysteps/master/environment_dev.yml -O /tmp/environment_dev.yml

# update base env
RUN conda-env update -n base -f /tmp/environment_dev.yml --prune && \
    conda clean --all -y
#
############# pySTEPS_devenv ########################################


############## DIRS #######################################
# Setup DATA_DIR directory
ENV DATA_DIR="/opt/data"
# Make
RUN mkdir $DATA_DIR

# Setup SRC_DIR directory
ENV SRC_DIR="/opt/src"
# Make
RUN mkdir $SRC_DIR
############## VOLS #######################################


############# pySTEPS ########################################
#
ARG gitUser=pySTEPS

RUN git clone https://github.com/$gitUser/pysteps $SRC_DIR

RUN pip install -e $SRC_DIR 
#
############# pySTEPS ########################################








