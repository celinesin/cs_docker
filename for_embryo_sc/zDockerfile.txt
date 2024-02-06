# Docker file to create image for ROADdt_embryo_sc
FROM jupyter/datascience-notebook:notebook-6.3.0

LABEL version="0.3.0"
LABEL description="Docker instance for ROADdt_embryo_sc (single cell analysis)"
LABEL maintainer="csin@cemm.oeaw.ac.at"

# generally useful things
USER root
RUN apt-get update
RUN apt-get -y install build-essential
RUN apt-get -y install python3-dev
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge

# install tools for single cell
RUN conda install numba==0.54.0
RUN pip install dynamo-release==1.2.0

# for pretty figures
RUN pip install matplotlib==3.5.3 palettable==3.3.0
COPY fonts /usr/share/fonts/truetype/
RUN fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf

# install network tools
RUN pip install ForceAtlas2==1.0 networkx==3.0
RUN pip install netcomp==0.2.3

# for netctrl
COPY igraph-0.8.5.tar.gz igraph-0.8.5.tar.gz
RUN tar -xf igraph-0.8.5.tar.gz
WORKDIR igraph-0.8.5
RUN ./configure
RUN make
RUN make install

COPY netctrl /usr/local/bin/
WORKDIR /home/jovyan

# install tools for genetics
RUN conda install -c bioconda samtools
RUN pip install mygene==3.2.2
RUN apt-get install bedtools


RUN pip install scanpy==1.9.1 python-igraph louvain
RUN pip install scanorama==1.7.1

# install velocyto
#RUN conda install numpy scipy cython matplotlib scikit-learn h5py click
RUN pip install leidenalg==0.9.0
#RUN pip install velocyto==0.17.17
#RUN pip install statsmodels==0.13.2
RUN pip install scikit-misc==0.1.4

# install scvi
RUN pip install torch==1.11.0
RUN pip install torchaudio==0.11.0
RUN pip install torchvision==0.12.0
RUN pip install pyYAML==5.4.1 --ignore-installed
RUN pip install scvi-tools==0.15.4
RUN pip install umap-learn==0.5.1

# install R things
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'
RUN Rscript -e "install.packages('Seurat', repos='http://cran.us.r-project.org/')"

# install CellOracle (https://morris-lab.github.io/CellOracle.documentation/installation/index.html#optional-make-a-new-environment)
#RUN conda install goatools pyarrow tqdm joblib
#RUN conda install gimmemotifs==0.14.4 genomepy==0.8.4
#RUN chmod 777 ~/.cache/gimmemotifs/
#RUN Rscript -e 'BiocManager::install(c("linkcomm", "rnetcarto"))'
#RUN pip install git+https://github.com/morris-lab/CellOracle.git
#RUN pip install leidenalg==0.8.4
RUN apt install -y libcurl4-openssl-dev
RUN apt install -y zlib1g
RUN pip install pyBigWig==0.3.18
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

# testing
RUN Rscript -e "install.packages('scLink', repos='http://cran.us.r-project.org/')"

RUN pip install cdlib==0.2.6

# jupyterproblem
RUN pip install markupsafe==2.0.1
