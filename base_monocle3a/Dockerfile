# Docker image for Monocle3alpha version

FROM jupyter/datascience-notebook:abdb27a6dfbb

# install monocle2
RUN Rscript -e "source("http://bioconductor.org/biocLite.R"); biocLite(); biocLite("monocle")"

# monocle3 alpha dependencies
RUN Rscript -e "devtools::install_github('cole-trapnell-lab/DDRTree', ref='simple-ppt-like'); devtools::install_github('cole-trapnell-lab/L1-graph')"

RUN Rscript -e "install.packages('reticulate'); library(reticulate); py_install('umap-learn', pip = T, pip_ignore_installed = T); py_install('louvain')"

RUN Rscript -e "devtools::install_github('cole-trapnell-lab/monocle-release', ref='monocle3_alpha')"