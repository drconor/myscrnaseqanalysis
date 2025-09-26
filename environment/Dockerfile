# hash:sha256:7d40d912b7a8ece9ec7359835f3e6c81dacfb32c6c82c0156be3638cfaaef7cb
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/py-r:python3.10.12-R4.2.3-IRkernel-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-askpass /

RUN mamba install -y --channel=bioconda \
        r-irkernel==1.3.2 \
        r-presto==1.0.0 \
        r-rcpp==1.0.11 \
        r-seurat==5.1.0 \
    && mamba clean -ya

ARG RCACHE_OPTIONS
RUN echo $RCACHE_OPTIONS >> $(Rscript -e 'cat(R.home())')/etc/Rprofile.site
RUN Rscript -e 'remotes::install_version("BiocManager", "1.30.26")' \
    && Rscript -e 'remotes::install_version("markdown", "2.0")'

RUN Rscript -e 'options(warn=2); install.packages("BiocManager")'
RUN Rscript -e 'options(warn=2); BiocManager::install(c( \
        "BiocVersion", \
        "limma" \
    ))' # Original versions: 3.16.0 3.54.2
