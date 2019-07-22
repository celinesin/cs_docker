# Docker file to create image for Velocyto
# http://velocyto.org/

FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker image for Velocyto"
LABEL maintainer="csin@cemm.oeaw.ac.at"


USER root
RUN ln -s /bin/tar /bin/gtar


# dependencies for velocyto
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install(); BiocManager::install('pcaMethods')"
# need internal unzip for install_github packages
RUN Rscript -e "options(unzip = 'internal'); devtools::install_github('hhoeflin/hdf5r')"
RUN sudo apt-get update
RUN sudo apt-get install -y libboost-all-dev
RUN ldconfig

RUN conda install -c bioconda samtools
RUN conda install numpy scipy cython numba matplotlib scikit-learn h5py click
RUN pip install velocyto

RUN mv /opt/conda/lib/R/etc/Makeconf /opt/conda/lib/R/etc/Makeconf_older
COPY Makeconf /opt/conda/lib/R/etc/Makeconf

RUN Rscript -e "library(devtools); options(unzip = 'internal'); install_github('velocyto-team/velocyto.R')"

RUN mv /opt/conda/lib/R/etc/Makeconf_older /opt/conda/lib/R/etc/Makeconf


