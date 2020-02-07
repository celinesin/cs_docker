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

# install R things
RUN Rscript -e "install.packages(c('BiocManager', 'devtools'), repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'

# install SCENIC (https://rawcdn.githack.com/aertslab/SCENIC/701cc7cc4ac762b91479b3bd2eaf5ad5661dd8c2/inst/doc/SCENIC_Setup.html)
RUN Rscript -e 'BiocManager::install(c("AUCell", "RcisTarget"))'
RUN Rscript -e 'BiocManager::install(c("GENIE3")) # Optional. Can be replaced by GRNBoost'
RUN Rscript -e 'BiocManager::install(c("zoo", "mixtools", "rbokeh"))'
RUN Rscript -e 'BiocManager::install(c("DT", "NMF", "pheatmap", "R2HTML", "Rtsne"))'
RUN Rscript -e 'BiocManager::install(c("doMC", "doRNG"))'
RUN Rscript -e 'devtools::install_github("aertslab/SCopeLoomR", build_vignettes = TRUE)'

# install pySCENIC
RUN pip install pyscenic