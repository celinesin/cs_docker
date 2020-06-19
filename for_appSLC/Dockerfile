# Docker file to create image for SLC genetic interactions project

## REPLACE
FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for appSLC"
LABEL maintainer="csin@cemm.oeaw.ac.at"



USER root
RUN apt-get update

# for apache/flask/etc
RUN apt-get install apache2
RUN apt-get install libapache2-mod-wsgi-py3 python3-dev
RUN a2enmod wsgi 

RUN apt-get install python3-pip
RUN pip3 install Flask 

# for analysis
RUN sudo pip3 install networkx
RUN sudo pip3 install numpy pandas scipy

# for dash stuff
RUN sudo pip3 install dash dash-html-components dash_cytoscape

# celine: get your shortcuts
# https://github.com/celinesin/cs_dotfiles.git
# https://github.com/menchelab/appSLC.git
# don't forget to switch to the right branch!


#RUN pip3 install gunicorn


