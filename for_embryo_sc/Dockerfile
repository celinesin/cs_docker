# Docker file to create image for ROADdt_embryo_sc
FROM quay.io/jupyter/pytorch-notebook:x86_64-cuda12-python-3.12.9

LABEL version="1.0.0"
LABEL description="Docker instance for ROADdt_embryo_sc (single cell analysis)"
LABEL maintainer="celine@lbi-netmed.com"

# generally useful things
USER root
RUN apt update
RUN apt-get update
RUN apt-get -y install build-essential
RUN apt-get -y install python3-dev

# for pretty figures
RUN pip install matplotlib==3.10.1 palettable==3.3.3
COPY fonts /usr/share/fonts/truetype/
RUN sudo fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf
RUN pip install plotly==6.0.1
RUN pip install kaleido==0.2.1
