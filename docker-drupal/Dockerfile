FROM ubuntu:16.04

# Bootstrap Ansible via pip
RUN apt-get update && apt-get install -y wget gcc make python python-dev python-setuptools python-pip libffi-dev libssl-dev libyaml-dev
RUN pip install -U pip
RUN pip install -U ansible

# Prepare Ansible environment
RUN mkdir /ansible#
COPY . /ansible

# Launch Ansible playbook from inside container
RUN cd /ansible && ansible-playbook container-provision.yml

# Cleanup
RUN rm -rf /ansible
#RUN for dep in $(pip show ansible | grep Requires | sed 's/Requires: //g; s/,//g'); do pip uninstall -y $dep; done
#RUN apt-get purge -y python-dev python-pip

# Install Drupal
RUN composer create-project drupal-composer/drupal-project:8.x-dev /var/www/drupal/ --stability dev --no-interaction
COPY settings.php.live /var/www/drupal/web/sites/default/settings.php

RUN apt-get autoremove -y && apt-get autoclean -y && apt-get clean -y
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp* /usr/share/doc/*

# Environment setup
WORKDIR /

ENTRYPOINT ["/usr/bin/supervisord"]