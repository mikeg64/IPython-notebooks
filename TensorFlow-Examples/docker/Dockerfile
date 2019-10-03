#docker image for datascience using jupyter with ubuntu

# Use the latest ubuntu image as base for the new image
# ubuntu is the image name and latest is a tag that 
# references a particular version of the image.
# In this case latest is always the latest LTS image
# at the time of writing this, it's 16.04.
FROM ubuntu:latest

# Run a system update to get it up to speed
# Then install python3 and pip3
RUN apt-get update && apt-get install -y apt-utils && apt-get install -y python3 \
    python3-pip python3-dev && apt-get install -y git-core && apt-get install -y curl && apt-get install -y wget

RUN apt-get install -y build-essential cmake git unzip pkg-config libopenblas-dev liblapack-dev

RUN apt-get update &&DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends tzdata && rm -rf /var/lib/apt/lists/*

#RUN apt-get install -y python-numpy python-scipy python-matplotlib python-yaml

# Install jupyter
RUN pip3 install numpy
RUN pip3 install scipy
RUN pip3 install jupyter
RUN pip3 install matplotlib
RUN pip3 install seaborn

RUN pip3 install pandas
RUN pip3 install -U scikit-learn
RUN pip3 install nltk
RUN pip3 install -U textblob
RUN pip3 install h5py

#RUN apt-get --fix-missing
#RUN add-apt-repository universe
RUN apt update
RUN apt-get install -y libhdf5-serial-dev python-h5py


RUN pip3 install pydot-ng

#RUN apt-get install -y graphviz
#RUN apt-get install -y python-opencv
RUN pip3 install tensorflow

RUN pip3 install keras

# Add Tini. Tini operates as a process subreaper for jupyter. This prevents
# kernel crashes.
ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]




# Create a new system user
RUN useradd -ms /bin/bash jupyter

# Change to this new user
USER jupyter

# Set the container working directory to the user home folder
WORKDIR /home/jupyter

RUN git clone https://github.com/mikeg2105/datascience-py

RUN ["mkdir", "notebooks"]
RUN ["mkdir", "data"]
#COPY *.py scripts 
#COPY *.csv scripts

#Jupyter
EXPOSE 8888
CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0"]
#CMD ["python3"]

#run using something like
#docker container run --rm -it mikeg64/python-datascience:3.0 /bin/sh
#docker container run -p 8888:8888 --rm -it mikeg64/python-datascience:3.0 python3 scripts/01_05.py >& out.csv


#start the docker container but mount a folder ~/proj/pyiome/python (for example) so that it can be accessed from /home/jupyter/data
#in the container

#docker run -v /Users/mikegriffiths/proj:/home/jupyter/notebooks --rm -p 8888:8888 mikeg64/tensorflow-examples

