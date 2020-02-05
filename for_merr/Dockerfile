# Docker file to create image for Merrit's data
FROM jupyter/datascience-notebook:7a0c7325e470

LABEL version="0.0.1"
LABEL description="Docker instance for Merrit's data"
LABEL maintainer="csin@cemm.oeaw.ac.at"

USER root

# install samtools
RUN conda install -c bioconda samtools

# install scanpy
RUN pip install scanpy python-igraph louvain

# install velocyto
RUN conda install numpy scipy cython numba matplotlib scikit-learn h5py click
RUN pip install velocyto

# install GENIE3
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e 'BiocManager::install("GENIE3")'
RUN Rscript -e 'update.packages(repos = "http://cran.us.r-project.org")'

# install other R things
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'