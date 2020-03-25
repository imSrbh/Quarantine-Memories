# SOURCE IMAGE
FROM s390x/ubuntu
MAINTAINER Saurabh Kumar Singh

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
