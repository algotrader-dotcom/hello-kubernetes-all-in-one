FROM ubuntu:16.04

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update

# Bootstrap Ansible via pip
#RUN apt-get update && apt-get install -y wget gcc make python python-dev python-setuptools python-pip libffi-dev libssl-dev libyaml-dev
#RUN pip install -U pip
#RUN pip install -U ansible

# Prepare Ansible environment
#RUN mkdir /ansible
#COPY . /ansible

# Launch Ansible playbook from inside container
# RUN cd /ansible && ansible-playbook container-provision.yml -v

# Cleanup
#RUN rm -rf /ansible
#RUN for dep in $(pip show ansible | grep Requires | sed 's/Requires: //g; s/,//g'); do pip uninstall -y $dep; done
#RUN apt-get purge -y python-dev python-pip
#RUN apt-get autoremove -y && apt-get autoclean -y && apt-get clean -y
#RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp* /usr/share/doc/*

# Environment setup
WORKDIR /

USER root

# ENTRYPOINT ["ls -la /"]
CMD ["/bin/bash"]