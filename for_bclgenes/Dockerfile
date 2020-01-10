# Docker file to create image for BCL gene lists project


FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for BCL gene lists project"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for general python usage
RUN pip install pandas     # included in base image, but needs update

# for ppi stuff
RUN pip install mygene
RUN apt-get install -y libmysqlclient-dev
RUN pip install mysqlclient

# for network layouts
RUN pip install ForceAtlas2