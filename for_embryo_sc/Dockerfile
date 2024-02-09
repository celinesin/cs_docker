# Docker file to create image for ROADdt_embryo_sc
FROM jupyter/datascience-notebook:2023-10-20

LABEL version="0.4.0"
LABEL description="Docker instance for ROADdt_embryo_sc (single cell analysis)"
LABEL maintainer="csin@cemm.oeaw.ac.at"

# generally useful things
USER root
RUN apt-get update
RUN apt-get -y install build-essential
RUN apt-get -y install python3-dev
RUN apt update
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge

# jupyterproblem
RUN pip install markupsafe==2.0.1

# for pretty figures
RUN pip install matplotlib==3.5.3 palettable==3.3.0
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# install tools for single cell
RUN pip install umap-learn==0.5.1
RUN pip install scikit-misc==0.3.1
RUN pip install 'scanpy[leiden]'==1.9.3

RUN pip install pyYAML==6.0.1 --ignore-installed
RUN pip install scvi-tools==0.15.4

#RUN pip install cdlib==0.2.6
#RUN conda install numba==0.54.0
RUN pip install dynamo-release==1.4.0
#RUN git clone https://github.com/aristoteleo/dynamo-release.git
#WORKDIR /home/jovyan/dynamo-release
#RUN git reset --hard ba43701c
#RUN pip install ../dynamo-release/


# install R things, seurat for coexpression networks
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'
RUN Rscript -e "install.packages('Seurat', repos='http://cran.us.r-project.org/')"
# testing
RUN Rscript -e "install.packages('scLink', repos='http://cran.us.r-project.org/')"

# install tools for genetics
RUN conda install -c bioconda samtools
RUN pip install mygene==3.2.2
RUN apt-get install bedtools

# install GRN packages
# cellOracle
RUN apt install -y libcurl4-openssl-dev
RUN apt install -y zlib1g
RUN pip install pyBigWig==0.3.18
RUN pip install gimmemotifs==0.18.0
RUN pip install celloracle==0.12.0

# install SCENIC (https://rawcdn.githack.com/aertslab/SCENIC/701cc7cc4ac762b91479b3bd2eaf5ad5661dd8c2/inst/doc/SCENIC_Setup.html)
RUN Rscript -e 'BiocManager::install(c("AUCell", "RcisTarget"))'
RUN Rscript -e 'BiocManager::install(c("GENIE3")) # Optional. Can be replaced by GRNBoost'
RUN Rscript -e 'BiocManager::install(c("zoo", "mixtools", "rbokeh"))'
RUN Rscript -e 'BiocManager::install(c("DT", "NMF", "pheatmap", "R2HTML", "Rtsne"))'
RUN Rscript -e 'BiocManager::install(c("doMC", "doRNG"))'
RUN Rscript -e 'devtools::install_github("aertslab/SCopeLoomR", build_vignettes = TRUE)'
# install pySCENIC
RUN pip install pyscenic==0.12.0

# install network tools
RUN git clone https://github.com/AminAlam/forceatlas2
# we do not use the original version from bhargavchippada/forceatlas2: incompatibility with python3.9+
WORKDIR forceatlas2
RUN git reset --hard f557c3c344a2ffd70697711de7e89245d2e7149c
RUN python setup.py install
RUN pip install networkx==3.0
RUN pip install netcomp==0.2.3

# for netctrl
COPY igraph-0.8.5.tar.gz igraph-0.8.5.tar.gz
RUN tar -xf igraph-0.8.5.tar.gz
WORKDIR igraph-0.8.5
RUN ./configure
RUN make
RUN make install
COPY netctrl /usr/local/bin/

# R and python interface
RUN pip install pyreadr==0.4.7
WORKDIR /home/jovyan
# for gimmemotifs
RUN chmod -R 777 /home/jovyan/.cache

# for cell chat
RUN Rscript -e 'install.packages("NMF", repos="http://cran.us.r-project.org/")'
RUN Rscript -e 'devtools::install_github("jokergoo/circlize@9b21578")'
RUN Rscript -e 'devtools::install_github("jokergoo/ComplexHeatmap@7d95ca5")'
RUN Rscript -e 'BiocManager::install("BiocNeighbors")'
RUN Rscript -e 'devtools::install_github("immunogenomics/presto@31dc97f")'
RUN apt install -y cmake
RUN Rscript -e 'devtools::install_github("astamm/nloptr@fb201fa")'
RUN Rscript -e 'devtools::install_github("lme4/lme4@5b7b27e",dependencies=TRUE)'
RUN Rscript -e 'install.packages(c("car", "rstatix", "ggpubr"), repos="http://cran.us.r-project.org/")'
RUN apt-get install -y gfortran
RUN apt-get -y install libglpk-dev libgmp-dev libxml2-dev
RUN conda install r-igraph
RUN Rscript -e 'install.packages("ggnetwork", repos="http://cran.us.r-project.org/")'
RUN Rscript -e 'devtools::install_github("jinworks/CellChat@499c742")'