# Anaconda and Jupyter Notebook server  
[Ref](https://www.continuum.io/blog/developer-blog/anaconda-and-docker-better-together-reproducible-data-science)

1. Install Anaconda
wget --quiet https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh -O ~/anaconda.sh  && \
/bin/bash ~/anaconda.sh -b -p /opt/conda && \ 
rm ~/anaconda.sh

2. Install Jupyter  
conda install jupyter -y --quiet 

3. start Jupyter server  
mkdir /opt/notebooks && /opt/conda/bin/jupyter notebook --notebook-dir=/opt/notebooks --ip='*' --port=8888 --no-browser
