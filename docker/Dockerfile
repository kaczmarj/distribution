FROM ubuntu:16.04

# Install CellProfiler dependencies
RUN apt-get update \
    && apt-get install -y software-properties-common \
    && add-apt-repository ppa:deadsnakes/ppa \
    && apt -y update \
    && apt install -y \
        python3.8-dev python3.8-distutils openjdk-8-jdk-headless \
        libmysqlclient-dev libnotify-dev libsdl2-dev libwebkitgtk-3.0 locales wget \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen en_US en_US.UTF-8

# Set up environment
RUN export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
RUN export PATH=$PATH:/home/ubuntu/.local/bin

# This is needed for a Python 3.8 quirk
RUN wget -q https://bootstrap.pypa.io/get-pip.py  \
    && python3.8 get-pip.py \
    && rm get-pip.py

#Install wx from a wheel
RUN wget -q https://extras.wxpython.org/wxPython4/extras/linux/gtk3/ubuntu-16.04/wxPython-4.1.0-cp38-cp38-linux_x86_64.whl \
    && python3.8 -m pip install --no-cache-dir wxPython-4.1.0-cp38-cp38-linux_x86_64.whl \
    && rm wxPython-4.1.0-cp38-cp38-linux_x86_64.whl

# Install CellProfiler
ARG version=4.2.0
RUN python3.8 -m pip install --no-cache-dir numpy cython
RUN python3.8 -m pip install --no-cache-dir cellprofiler==$version

WORKDIR /work
ENTRYPOINT ["cellprofiler"]

CMD ["--run", "--run-headless", "--help"]
