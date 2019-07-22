# Docker file to create image for Monocle3 0.1.0 and velocyto

FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for analysing single cell RNA-Seq data"
LABEL maintainer="csin@cemm.oeaw.ac.at"
LABEL maintainer="mhaimel@cemm.oeaw.ac.at"
LABEL monocle3.version="0.1.0"


USER root
RUN ln -s /bin/gzip /usr/bin/gzip
RUN ln -s /bin/tar /bin/gtar

RUN conda install -c bioconda samtools