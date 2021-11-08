FROM 4dndcic/ubuntu16.04-miniconda-python36:v1
MAINTAINER Soo Lee (duplexa@gmail.com), Michele Berselli (berselli.michele@gmail.com)

# general updates & installing necessary Linux components
RUN apt-get update -y && apt-get install -y \
    bzip2 \
    gcc \
    g++ \
    git \
    less \
    libncurses-dev \
    make \
    time \
    zip \
    unzip \
    vim \
    wget \
    zlib1g-dev \
    liblz4-tool \
    libbz2-dev \
    liblzma-dev \
    locales \
    parallel \
    autoconf \
    autogen \
    autotools-dev \
    automake \
    pkg-config \
    tabix \
    yasm \
    libdbi-perl \
    libmodule-build-perl \
    libarchive-zip-perl \
    libmysqlclient-dev \
    libpng-dev \
    libexpat1-dev

WORKDIR /usr/local/bin

# gatk4 & picard & python libraries
RUN conda install -c bioconda -y gatk4==4.1.2.0 picard==2.20.2 \
    pysam==0.15.3 python=3.6.8 && \
    conda clean -a -y -f

# samtools
RUN wget https://github.com/samtools/samtools/releases/download/1.9/samtools-1.9.tar.bz2 && \
    tar -xjf samtools-1.9.tar.bz2 && \
    rm -rf samtools-1.9.tar.bz2 && \
    cd samtools-1.9 && \
    ./configure && \
    make && \
    cd .. && \
    ln -s samtools-1.9 samtools

# bwa
RUN wget https://github.com/lh3/bwa/archive/v0.7.17.tar.gz && \
    tar -xzf v0.7.17.tar.gz && \
    rm -rf v0.7.17.tar.gz && \
    cd bwa-0.7.17 && \
    make && \
    cd .. && \
    ln -s bwa-0.7.17 bwa

# pigz
RUN wget https://zlib.net/pigz/pigz-2.6.tar.gz && \
    tar -xzf pigz-2.6.tar.gz && \
    rm -rf pigz-2.6.tar.gz && \
    cd pigz-2.6 && \
    make && \
    cd .. && \
    ln -s pigz-2.6 pigz

# pbgzip
RUN git clone https://github.com/nh13/pbgzip && \
    mv pbgzip pbgzip-dir && \
    cd pbgzip-dir && \
    git checkout 2b09f97 && \
    cd igzip && \
    make && \
    make install && \
    cd .. && \
    sh autogen.sh && \
    ./configure --enable-igzip && \
    make && \
    make install && \
    cd .. && \
    rm -rf pbgzip-dir

ENV LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH

# bwa mem script
COPY bwa-mem-to-bam.sh .
RUN chmod +x bwa-mem-to-bam.sh

COPY bwa-mem-to-bam_no_unzip.sh .
RUN chmod +x bwa-mem-to-bam_no_unzip.sh

# bam integrity check script
COPY integrity-check.sh .
RUN chmod +x integrity-check.sh

# add read groups script
RUN git clone https://github.com/dbmi-bgm/cgap-scripts/ && \
    cd cgap-scripts && \
    git checkout 28520db && \
    chmod +x AddReadGroups.py && \
    chmod +x split_bam.py && \
    cd ..

# bamqc
COPY scripts/bamqc.py .
RUN chmod +x bamqc.py

# ApplyBQSR parallel
COPY ApplyBQSR-parallel.sh .
RUN chmod +x ApplyBQSR-parallel.sh

# env paths
ENV PATH=/usr/local/bin/samtools/:$PATH
ENV PATH=/usr/local/bin/bwa/:$PATH
ENV PATH=/usr/local/bin/cgap-scripts/:$PATH
ENV PATH=/usr/local/bin/pigz/:$PATH

# supporting UTF-8
RUN locale-gen "en_US.UTF-8" && update-locale LC_ALL="en_US.UTF-8"
ENV LC_ALL=en_US.UTF-8

CMD ["bash"]
