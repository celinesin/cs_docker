# Docker file to create image for Monocle3 0.1.0 and velocyto

FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.4"
LABEL description="Docker instance for analysing single cell RNA-Seq data"
LABEL maintainer="csin@cemm.oeaw.ac.at"
LABEL maintainer="mhaimel@cemm.oeaw.ac.at"
# similar to 0.1.2
LABEL monocle3.version="45f57a0" 


USER root
RUN ln -s /bin/gzip /usr/bin/gzip
RUN ln -s /bin/tar /bin/gtar

RUN apt-get update
RUN apt-get install -y libudunits2-dev
RUN conda install -c bioconda bioconductor-hdf5array
RUN conda install -c r r-reticulate

# Monocle
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e "BiocManager::install(c('SingleCellExperiment', 'SummarizedExperiment', 'DelayedMatrixStats', 'limma', 'BiocGenerics', 'DelayedArray', 'S4Vectors'))"
RUN Rscript -e "install.packages('spData', repos='http://cran.us.r-project.org/')"
RUN conda install -c conda-forge r-udunits2 
RUN apt-get install -y libgdal-dev
RUN conda install -c conda-forge gdal 
RUN conda install -c conda-forge r-gdalutils
RUN conda install -c r r-gdata
RUN conda install -c conda-forge r-spdep

RUN Rscript -e "options(unzip = 'internal'); install.packages('units', repos='http://cran.us.r-project.org/', type = 'source')"
RUN conda install -c conda-forge r-sf

RUN Rscript -e "options(unzip = 'internal'); install.packages('spdep', repos='http://cran.us.r-project.org/')"
RUN conda install -c vtraag louvain
#RUN Rscript -e "install.packages('reticulate', repos='http://cran.wu.ac.at/'); 
RUN Rscript -e "library(reticulate); conda_create('r-reticulate'); reticulate::py_install('louvain')"
RUN Rscript -e "options(unzip = 'internal'); devtools::install_github('cole-trapnell-lab/monocle3', ref='45f57a0')"

# Seurat
RUN Rscript -e "install.packages('Seurat', repos='http://cran.wu.ac.at/')"

# Velocyto

RUN Rscript -e "BiocManager::install('pcaMethods')"
RUN Rscript -e "options(unzip = 'internal'); devtools::install_github('hhoeflin/hdf5r')"
RUN sudo apt-get update
RUN sudo apt-get install -y libboost-all-dev
RUN ldconfig
RUN sudo apt-get install -y libbz2-dev

RUN conda install numpy scipy cython numba matplotlib scikit-learn h5py click
RUN pip install loompy
RUN conda install -c bioconda pysam 
RUN pip install velocyto

RUN mv /opt/conda/lib/R/etc/Makeconf /opt/conda/lib/R/etc/Makeconf_older
COPY Makeconf /opt/conda/lib/R/etc/Makeconf

RUN Rscript -e "library(devtools); options(unzip = 'internal'); install_github('velocyto-team/velocyto.R')"

RUN mv /opt/conda/lib/R/etc/Makeconf_older /opt/conda/lib/R/etc/Makeconf


# additional tools
RUN conda install -c bioconda samtools
RUN conda install -c r r-xlsx


# SCENIC
RUN pip install pyscenic