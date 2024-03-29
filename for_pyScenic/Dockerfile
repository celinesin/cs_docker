# Docker file to create image for pySCENIC


FROM jupyter/datascience-notebook:abdb27a6dfbb

LABEL version="0.0.1"
LABEL description="Docker instance for analysing single cell RNA-Seq data"
LABEL maintainer="csin@cemm.oeaw.ac.at"
LABEL maintainer="mhaimel@cemm.oeaw.ac.at"
LABEL monocle3.version="0.1.0"


USER root
RUN ln -s /bin/tar /bin/gtar

ENV DEBIAN_FRONTEND=noninteractive
RUN BUILDPKGS="build-essential apt-utils \
        python3-dev libhdf5-dev libfreetype6-dev libtool \
        m4 autoconf automake patch bison flex libpng-dev libopenblas-dev \
        tcl-dev tk-dev libxml2-dev zlib1g-dev libffi-dev cmake" && \
    apt-get update && \
    apt-get install -y debconf locales && dpkg-reconfigure locales && \
    apt-get install -y $BUILDPKGS && \
    ### run time:
    apt-get install -y zlib1g hdf5-tools gfortran libgcc1 libstdc++ musl \
        libopenblas-base tcl tk libxml2 libffi6 less procps

# install dependencies:
COPY requirements_docker.txt /tmp/
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r /tmp/requirements_docker.txt

# use version from argument (--build-arg version=0.9.7), or a default:
ARG version="0.9.15"
RUN pip install --no-cache-dir pyscenic==$version && \
    pip install --no-cache-dir scanpy==1.4.4

RUN apt-get remove --purge -y $BUILDPKGS && \
    rm -rf /var/lib/apt/lists/*