# Docker file to create image for ROADdt_embryo_sc
FROM quay.io/jupyter/pytorch-notebook:x86_64-cuda12-python-3.11.8
# https://github.com/jupyter/docker-stacks/wiki

LABEL version="1.0.0"
LABEL description="Docker instance for ROADdt_embryo_sc (single cell analysis)"
LABEL maintainer="celine@lbi-netmed.com"



# generally useful things
USER root
RUN apt update
RUN apt install -y cmake
RUN apt-get update
RUN apt-get -y install build-essential
RUN apt-get -y install python3-dev
RUN apt-get -y install r-base
RUN apt-get -y install libcurl4-openssl-dev libssl-dev
RUN conda config --add channels defaults
RUN conda config --add channels bioconda
RUN conda config --add channels conda-forge
RUN conda config --add channels r


# for pretty figures
RUN pip install matplotlib==3.10.1 palettable==3.3.3
COPY fonts /usr/share/fonts/truetype/
RUN sudo fc-cache -fv
RUN rm /home/jovyan/.cache/matplotlib -rf
RUN pip install plotly==6.0.1
RUN pip install kaleido==0.2.1

# for big data
RUN pip install umap-learn==0.5.7
RUN pip install scikit-misc==0.5.1
RUN pip install optuna==4.1.0
RUN pip install RapidFuzz==3.12.2

# install network tools
RUN pip install fa2-modified==0.3.10
RUN pip install networkx==3.4.2
RUN pip install python-louvain==0.16
RUN pip install teneto==0.5.3
RUN pip install networkx-temporal[draw]==1.2.1
RUN pip install reticula==0.13.0

# for netctrl
RUN pip install igraph==0.11.8
COPY netctrl /usr/local/bin/

# install tools for genetics
RUN mamba install -c bioconda python=3.11.8 samtools
RUN pip install mygene==3.2.2
RUN apt-get install bedtools
RUN pip install gseapy==1.1.7

# install tools for single cell
RUN pip install scanpy[leiden]==1.11.0
RUN pip install pyYAML==6.0.2
RUN pip install scvi-tools==1.2.1
RUN pip install dynamo-release==1.4.1
RUN pip install cellrank==2.0.4
RUN pip install moscot==0.4.2

# install GRN packages
# cellOracle
RUN apt install -y libcurl4-openssl-dev
RUN apt install -y zlib1g
RUN pip install pyBigWig==0.3.24
RUN pip install gimmemotifs==0.17.2
# for gimmemotifs
RUN chmod -R 777 /home/jovyan/.cache
RUN pip install git+https://github.com/morris-lab/CellOracle.git@a1c1bbf

# scenic plus
RUN pip install git+https://github.com/aertslab/scenicplus@v1.0a2




# install R things
RUN mamba install -y r-irkernel
RUN Rscript -e "install.packages('BiocManager', repos='http://cran.us.r-project.org/'); BiocManager::install();"
RUN apt-get install -y libfontconfig1-dev libharfbuzz-dev libfribidi-dev
RUN apt-get install -y libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev
RUN mamba install -c conda-forge pkg-config
RUN Rscript -e 'install.packages("devtools", repos="http://cran.us.r-project.org/")'

# R and python interface
RUN pip install pyreadr==0.4.7




# R single cell tools
RUN Rscript -e 'BiocManager::install("SingleCellExperiment")'
RUN Rscript -e "install.packages('Seurat', version='5.2.1', repos='http://cran.us.r-project.org/')"
RUN Rscript -e "install.packages('scLink', repos='http://cran.us.r-project.org/')"

# for cell chat | needs cmake
RUN Rscript -e 'install.packages("NMF", repos="http://cran.us.r-project.org/")'
RUN Rscript -e 'devtools::install_github("jokergoo/circlize@9b21578")'
RUN Rscript -e 'devtools::install_github("jokergoo/ComplexHeatmap@7d95ca5")'
RUN Rscript -e 'BiocManager::install("BiocNeighbors")'
RUN Rscript -e 'devtools::install_github("immunogenomics/presto@31dc97f")'
RUN Rscript -e 'devtools::install_github("astamm/nloptr@fb201fa")'
RUN Rscript -e 'devtools::install_github("lme4/lme4@5b7b27e",dependencies=TRUE)'
RUN Rscript -e 'install.packages(c("car", "rstatix", "ggpubr"), repos="http://cran.us.r-project.org/")'
RUN apt-get install -y gfortran
RUN apt-get -y install libglpk-dev libgmp-dev libxml2-dev
RUN mamba install r-igraph
RUN Rscript -e 'install.packages("ggnetwork", repos="http://cran.us.r-project.org/")'
RUN Rscript -e 'devtools::install_github("jinworks/CellChat@499c742")'

# for nischenetr
RUN Rscript -e 'BiocManager::install("limma")'
RUN Rscript -e 'devtools::install_github("saeyslab/nichenetr@dd7a859")'

# create folders for bind points
RUN mkdir /home/jovyan/op_velocyto
RUN mkdir /home/jovyan/op_velocyto/00big

WORKDIR /home/jovyan/

RUN mamba info -a