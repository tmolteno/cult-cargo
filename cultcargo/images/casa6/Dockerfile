FROM {REGISTRY}/base-cult:{BUNDLE_VERSION}

RUN apt-get update && apt-get -y upgrade && \
    apt-get -y install xvfb python3-casacore python3-pip libblas-dev liblapack-dev \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /var/cache/apt/archives 

RUN pip install --no-cache-dir --upgrade numpy casatools=={wheel_version} casatasks=={wheel_version} casaconfig casadata

RUN mkdir -p /opt/casa/data

COPY casasiteconfig.py /opt/casa

ENV CASASITECONFIG /opt/casa/casasiteconfig.py

RUN {python} -m casaconfig --measurespath /opt/casa/data --update-all

RUN {python} -m casaconfig --measurespath /opt/casa/data --current-data

RUN ln -s /usr/bin/{python} /usr/bin/python  

CMD /usr/bin/python
