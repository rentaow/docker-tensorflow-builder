FROM nvidia/cuda:9.1-runtime-centos7

COPY bazel.repo /etc/yum.repos.d/
RUN yum install bazel

# Install Anaconda
WORKDIR /
RUN wget "https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh" -O "miniconda.sh" && \
    bash "miniconda.sh" -b -p "/conda" && \
    rm miniconda.sh && \
    echo PATH='/conda/bin:$PATH' >> /root/.bashrc && \
    /conda/bin/conda config --add channels conda-forge && \
    /conda/bin/conda update --yes -n base conda && \
    /conda/bin/conda update --all --yes && \
    /conda/bin/conda install --yes numpy wheel

RUN ln -s /conda/bin/python /usr/bin/python

# Remove previous Cuda and cuDNN installation
RUN rm -fr /usr/local/cuda*
RUN find / -name *cudnn* -exec rm {} +

COPY build.sh /build.sh

ENTRYPOINT bash