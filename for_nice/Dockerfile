# Docker file to create image for SLC genetic interactions project

FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for SLC genetic interactions project"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for database stuff
RUN apt-get install -y libmysqlclient-dev
RUN pip install mysqlclient

RUN pip install mygene umap-learn

# for data manipulation
RUN pip install openpyxl

# for pretty figures
RUN pip install matplotlib==3.1.1 palettable
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# for dash stuff
RUN pip install gunicorn dash_cytoscape

# for felix pipeline
RUN pip install prettytable networkx dash==1.7.0 fisher
