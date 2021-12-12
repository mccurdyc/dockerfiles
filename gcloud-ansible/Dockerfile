FROM google/cloud-sdk:366.0.0-alpine

ENV ANSIBLE_VERSION 5.0.1
ENV DEBIAN_FRONTEND=noninteractive

ENV BUILD_PACKAGES \
  openssh-client \
  sshpass \
  shadow \
  curl \
  python3 \
  py3-dateutil \
  py3-httplib2 \
  py3-jinja2 \
  py3-paramiko \
  py3-pip \
  py3-yaml \
  ca-certificates

RUN apk update && apk upgrade && \
    apk add --no-cache ${BUILD_PACKAGES} && \
    pip install --upgrade pip && \
    pip install ansible==${ANSIBLE_VERSION} && \
    pip install google-auth && \
    rm -rf /var/cache/apk/*

ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING false
ENV ANSIBLE_RETRY_FILES_ENABLED false
ENV ANSIBLE_ROLES_PATH /ansible/playbooks/roles
ENV ANSIBLE_SSH_PIPELINING True
ENV PYTHONPATH /ansible/lib
ENV PATH /ansible/bin:$PATH
ENV ANSIBLE_LIBRARY /ansible/library
ENV GOOGLE_APPLICATION_CREDENTIALS /home/root/.config/gcloud/application_default_credentials.json

WORKDIR /ansible

COPY . .

CMD ["ansible-playbook"]
