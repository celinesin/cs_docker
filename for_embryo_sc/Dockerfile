# Docker file to create image for ROADdt_embryo_sc
FROM jupyter/datascience-notebook:notebook-6.3.0

LABEL version="0.3.0"
LABEL description="Docker instance for ROADdt_embryo_sc (single cell analysis)"
LABEL maintainer="csin@cemm.oeaw.ac.at"

# generally useful things
USER root
RUN apt-get update
RUN apt-get -y install build-essential
RUN apt-get -y install python3-dev
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge

# jupyterproblem
RUN pip install markupsafe==2.0.1

# for pretty figures
RUN pip install matplotlib==3.5.3 palettable==3.3.0
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# install tools for single cell
RUN pip install 'scanpy[leiden]'==1.9.3
RUN pip install scvi-tools==0.15.4
RUN conda install numba==0.54.0
RUN pip install dynamo-release==1.2.0



