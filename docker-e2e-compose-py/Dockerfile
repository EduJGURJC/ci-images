FROM elastest/ci-docker-e2e-compose:latest

LABEL maintainer "elastest-users@googlegroups.com"
LABEL version="0.1.0"
LABEL description="Builds a docker-in-docker e2e image that includes python 3.6 & test requirements."

USER root

RUN apt-get install -y \
    less \
    man \
    python \
    python-pip \
    python-virtualenv \
    unzip \
    vim
	
RUN add-apt-repository ppa:jonathonf/python-3.6 \
    && apt-get update \
    && apt-get install -y python3.6 python3-pip python3.6-dev build-essential libbz2-dev libssl-dev libreadline-dev libsqlite3-dev tk-dev libevent-dev \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3.6 10 \
    && pip install --upgrade pip flask_testing coverage nose pluggy py randomize tox tox-docker pyyaml \
    && pip install selenium

ENV WORKSPACE /home/jenkins

USER jenkins 

WORKDIR ${WORKSPACE}

# launch container
CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
