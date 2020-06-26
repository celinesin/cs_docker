# Docker file to create image for precisePID

FROM jupyter/datascience-notebook:04f7f60d34a6


LABEL version="0.0.1"
LABEL description="Docker instance for precisePID"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for database stuff
RUN pip install mygene
RUN apt-get install -y libmysqlclient-dev
RUN pip install mysqlclient

# for data manipulation
RUN pip install openpyxl

# for pretty figures
RUN pip install matplotlib==3.1.1 palettable
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# for analysis
RUN pip install networkx
RUN pip install scikit-learn numba
RUN pip install umap-learn umap-learn[plot]
RUN pip install scikit-learn

