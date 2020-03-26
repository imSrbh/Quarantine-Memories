FROM python:3.6-slim
RUN pip install jupyter numpy matplotlib

RUN mkdir demo/
WORKDIR demo/
COPY . .

WORKDIR src/
RUN python3 data_pipeline.py
RUN rm data/raw_data.csv
WORKDIR /demo


ENV TINI_VERSION v0.6.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
RUN chmod +x /usr/bin/tini
ENTRYPOINT ["/usr/bin/tini", "--"]

CMD ["jupyter", "notebook", "--port=8888", "--no-browser", "--ip=0.0.0.0", "--allow-root", "NotebookApp.token='smartcow'"]
etc


# SOURCE IMAGE
FROM s390x/ubuntu
MAINTAINER Mihai Criveti

# ADD AND RUN (python3, pip, jupyter notebook and redis module)
RUN apt-get update \
    && apt-get install -y python3 python3-pip \
    && pip3 install jupyter redis \
    && apt-get clean


# PERSISTENCE
VOLUME ["/notebooks"]

# WORKDIR
WORKDIR /notebooks

# COMMAND and ENTRYPOINT:
CMD ["jupyter","notebook","--allow-root","--ip=0.0.0.0","--port=9000"]

# NETWORK
EXPOSE 9000
