# 使用NVIDIA CUDA基础镜像
FROM nvidia/cuda:11.8.0-base-ubuntu22.04

# 设置环境变量
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ENV PATH /opt/conda/bin:$PATH

# 安装基本依赖
RUN apt-get update --fix-missing && \
    apt-get install -y wget bzip2 build-essential ca-certificates \
    libglib2.0-0 libxext6 libsm6 libxrender1 git && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# 下载并安装Miniconda
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh && \
    ln -s /opt/conda/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". /opt/conda/etc/profile.d/conda.sh" >> ~/.bashrc && \
    echo "conda activate base" >> ~/.bashrc

# 更新conda并安装常用包
RUN conda update -n base -c defaults conda && \
    conda install -y python=3.9 numpy pandas scipy scikit-learn matplotlib jupyter && \
    conda clean -a -y

# 设置工作目录
WORKDIR /workspace

# 暴露Jupyter Notebook端口
EXPOSE 8888

# 启动Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]
