# Docker file to create image for ROADdt_embryo_net
FROM jupyter/datascience-notebook:notebook-6.1.6

LABEL version="0.3.0"
LABEL description="Docker instance for ROADdt_embryo_net"
LABEL maintainer="csin@cemm.oeaw.ac.at"

# generally useful things
USER root
RUN apt-get update
RUN apt-get install build-essential
RUN apt-get -y install python3-dev
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge

# for pretty figures
RUN pip install matplotlib==3.1.1 palettable==3.3.0
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# install network tools
RUN pip install ForceAtlas2==1.0 networkx==1.11
RUN pip install netcomp==0.2.3

# for netctrl
COPY igraph-0.8.5.tar.gz igraph-0.8.5.tar.gz
RUN tar -xf igraph-0.8.5.tar.gz
WORKDIR igraph-0.8.5
RUN ./configure
RUN make
RUN make install

COPY netctrl /usr/local/bin/
WORKDIR /home/jovyan

# install analysis tools
RUN pip install scikit-learn==1.1.2

# install tools for genetics
RUN conda install -c bioconda samtools
RUN pip install mygene==3.2.2
RUN apt-get install bedtools


# jupyterproblem
RUN pip install markupsafe==2.0.1
