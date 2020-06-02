# Docker file to create image for SLC genetic interactions project


FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for SLC genetic interactions project"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for apache/flask/etc
RUN apt-get install apache2
RUN apt-get install libapache2-mod-wsgi-py3 python-dev
RUN a2enmod wsgi 
RUN pip install Flask 

# for analysis
RUN pip install networkx
RUN pip install numpy pandas scipy

# for dash stuff
RUN pip install dash dash-html-components dash_cytoscape
RUN pip install gunicorn


