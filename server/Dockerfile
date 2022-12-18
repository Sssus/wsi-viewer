# Ubuntu 20.04 + nvidia/cuda + miniconda

FROM python:3.8-slim 
ENV LANG C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive

# Install Linux Package

RUN apt-get update && \
    apt-get -y install gcc mono-mcs && \
    apt-get -y install openslide-tools && \
    apt-get install -y wget vim curl && \
    apt-get clean

# Install Python Package

ADD ./requirements.txt /tmp/requirements.txt
RUN pip install --trusted-host ftp.daumkakao.com \
    --index-url http://ftp.daumkakao.com/pypi/simple -r /tmp/requirements.txt --no-cache-dir

#ADD ../src /
WORKDIR /workspace/
#EXPOSE 5000
#CMD ["python", "deepzoom_server.py"]
