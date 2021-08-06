# Docker file to create image for radipop

FROM jupyter/datascience-notebook:04f7f60d34a6


LABEL version="0.0.1"
LABEL description="Docker instance for radipop"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root
RUN apt-get update

# for data manipulation
RUN pip install openpyxl

# for pretty figures
RUN pip install matplotlib==3.1.1 palettable
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# for image analysis
RUN pip install pyradiomics
RUN pip install combat
RUN pip install scikit-learn numba
RUN pip install umap-learn 
RUN pip install umap-learn[plot]
RUN pip install holoviews[all]

RUN sudo apt-get install plastimatch
