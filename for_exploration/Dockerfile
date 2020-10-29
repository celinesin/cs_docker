# Docker file to create image for exploration

FROM jupyter/datascience-notebook:04f7f60d34a6


LABEL version="0.0.1"
LABEL description="Docker instance for exploration"
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
RUN pip install seaborn

# for analysis
RUN pip install networkx
RUN pip install scikit-learn numba
RUN pip install umap-learn umap-learn[plot]

