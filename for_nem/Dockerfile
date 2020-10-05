# Docker file to create image for network essentiality metric project


#FROM jupyter/datascience-notebook:abdb27a6dfbb
FROM jupyter/datascience-notebook:04f7f60d34a6


LABEL version="0.0.1"
LABEL description="Docker instance for network essentiality metric project"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for database stuff
RUN pip install mygene

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
RUN pip install umap-learn 
RUN pip install umap-learn[plot]

# for pySCENIC
RUN pip install pyscenic==0.10.0
RUN pip install fsspec>=0.3.3
RUN pip install dask[dataframe] --upgrade
RUN pip install distributed -U

