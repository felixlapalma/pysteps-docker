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


############# pySTEPS ########################################

# Set channels priority
RUN conda config --env --prepend channels conda-forge
RUN conda config --env --set channel_priority strict

# update base env
RUN conda install -n base -c conda-forge pysteps --prune && \
    conda clean --all -y
#
############# pySTEPS ########################################


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









