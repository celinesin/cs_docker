# Docker file to create image for Merrit's data (can't use 6.1.6 bc gimmemotifs na py3.8)
FROM jupyter/datascience-notebook:notebook-6.1.6

LABEL version="0.2.0"
LABEL description="Docker instance for Merrit's data"
LABEL maintainer="csin@cemm.oeaw.ac.at"

# generally useful things
USER root
RUN apt-get update
RUN apt-get install build-essential
RUN apt-get -y install python3-dev
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge

# for pretty figures
RUN pip install matplotlib==3.1.1 palettable
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# install network tools
RUN pip install ForceAtlas2 networkx

# for netctrl
COPY igraph-0.8.5.tar.gz igraph-0.8.5.tar.gz
RUN tar -xf igraph-0.8.5.tar.gz
WORKDIR igraph-0.8.5
RUN ./configure
RUN make
RUN make install

COPY netctrl /usr/local/bin/
WORKDIR /home/jovyan

# install samtools
# RUN conda install -c bioconda samtools==1.11

# install scanpy
RUN pip install scanpy python-igraph louvain

# install velocyto
RUN conda install numpy scipy cython numba matplotlib scikit-learn h5py click
RUN pip install velocyto

# install R things
RUN Rscript -e "install.packages(c('BiocManager', 'devtools'), repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'
RUN Rscript -e 'devtools::install_github(repo = "satijalab/seurat")'

# install SCENIC (https://rawcdn.githack.com/aertslab/SCENIC/701cc7cc4ac762b91479b3bd2eaf5ad5661dd8c2/inst/doc/SCENIC_Setup.html)
RUN Rscript -e 'BiocManager::install(c("AUCell", "RcisTarget"))'
RUN Rscript -e 'BiocManager::install(c("GENIE3")) # Optional. Can be replaced by GRNBoost'
RUN Rscript -e 'BiocManager::install(c("zoo", "mixtools", "rbokeh"))'
RUN Rscript -e 'BiocManager::install(c("DT", "NMF", "pheatmap", "R2HTML", "Rtsne"))'
RUN Rscript -e 'BiocManager::install(c("doMC", "doRNG"))'
RUN Rscript -e 'devtools::install_github("aertslab/SCopeLoomR", build_vignettes = TRUE)'

# install pySCENIC
RUN pip install pyscenic

# install CellOracle (https://morris-lab.github.io/CellOracle.documentation/installation/index.html#optional-make-a-new-environment)
RUN sudo chown 0:0 /opt/conda/pkgs/cache/a0b50a38.json
RUN conda install goatools pyarrow tqdm joblib
RUN apt-get -y install libcurl4-openssl-dev
RUN pip install pyBigWig
RUN pip install gimmemotifs==0.15.3
RUN Rscript -e 'BiocManager::install(c("linkcomm", "rnetcarto"))'
RUN pip install genomepy leidenalg ipyvuetify
RUN pip install git+https://github.com/morris-lab/CellOracle.git


