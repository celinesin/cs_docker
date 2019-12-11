# Docker file to create image for Merrit's data
FROM jupyter/datascience-notebook:7a0c7325e470

LABEL version="0.0.1"
LABEL description="Docker instance for Merrit's data"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root

# install scanpy
RUN pip install scanpy python-igraph louvain

# install palantir
RUN pip install git+https://github.com/jacoblevine/phenograph.git
RUN git clone git://github.com/dpeerlab/Palantir.git
RUN cd Palantir; pip install .

# install stream
RUN conda config --add channels defaults
RUN conda config --add channels conda-forge
RUN conda config --add channels bioconda
RUN apt-get update && apt-get install gsl-bin libgsl0-dev -y && apt-get clean
RUN conda install libgfortran stream=0.4.0 tzlocal -y && conda clean --all -y
RUN Rscript -e 'install.packages("stringi",repos="https://cloud.r-project.org/")'

# install dynamo
RUN git clone git://github.com/aristoteleo/dynamo-release.git
RUN pip install dynamo-release/.