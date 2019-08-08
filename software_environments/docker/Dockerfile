FROM nvidia/cuda:10.0-base

# install miniconda - copy bulk of conda docker file
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 ca-certificates curl git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-4.5.11-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    /opt/conda/bin/conda clean -tipsy && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate" >> ~/.bashrc

ENV BASH_ENV ~/.bashrc
SHELL ["/bin/bash", "-c"]
ENTRYPOINT ["/bin/bash", "-c"]

# start with new things - specific to the indaba

# install the add-apt-repository command
RUN apt-get update && \
    apt-get install -y software-properties-common dirmngr apt-transport-https lsb-release

# enable the universe repo
RUN add-apt-repository -y "deb http://archive.ubuntu.com/ubuntu $(lsb_release -sc) universe"

# install specific versoins of required python packages
RUN conda install numpy=1.16.4
RUN conda install jupyter=1.0.0
RUN conda install matplotlib=3.0.3
RUN pip install tensorflow-gpu==2.0.0-beta0

WORKDIR /sandbox

CMD ["bash"]
