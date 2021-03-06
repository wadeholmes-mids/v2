# Dockerfile for homework 6

# docker build -t hw06 .
# nvidia-docker run --rm --name hw06 -p 8888:8888 -d hw06

# point your browser to http://ip:8888/notebooks/v2/week06/hw/BERT_classifying_toxicity.ipynb

# FROM pytorch/pytorch:1.1.0-cuda10.0-cudnn7.5-devel
FROM pytorch/pytorch:1.5-cuda10.1-cudnn7-devel
RUN apt-get -y update
# necessary to make add_user.sh work
RUN apt-get install -y --fix-missing sudo
# stuff opencv complains if they are not installed
RUN apt-get install -y --fix-missing \
    libsm6 \
    libxext6 \
    libxrender-dev \
    libgtk2.0-dev \
    libavcodec-dev \
    libavformat-dev \
    libswscale-dev \
    wget
RUN apt-get clean && rm -rf /tmp/* /var/tmp/*
RUN pip --no-cache-dir install \
opencv-python \
scikit-image
RUN pip install jupyter
RUN pip install seaborn
RUN pip install nltk
RUN pip install pandas
RUN pip install scikit-learn
RUN pip install tensorflow-gpu
RUN pip install keras

RUN apt install -y git
RUN git clone https://github.com/NVIDIA/apex.git && cd apex && python setup.py install --cuda_ext --cpp_ext && cd ..
# RUN pip install pytorch-pretrained-bert
RUN pip install transformers

WORKDIR /root

RUN git clone https://github.com/MIDS-scaling-up/v2
WORKDIR /root/v2/week06/hw/data

RUN sh download.sh
WORKDIR /root 

EXPOSE 8888
CMD jupyter notebook  --no-browser --ip=0.0.0.0 --allow-root
