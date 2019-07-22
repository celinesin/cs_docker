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
RUN Rscript -e "options(unzip = 'internal'); devtools::install_github('cole-trapnell-lab/monocle3', ref='0.1.0')"
