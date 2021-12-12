# gcloud-ansible

This is a Docker image that uses `google/cloud-sdk:alpine` as the base image and
installs Ansible with the goal being of being able to generate a dynamic Ansible
inventory from GCP.

## Setup

If you want, you could create a shell alias. For example, I have
`gcloud-ansible` that looks like the following:

```bash
function gcloud-ansible() {
  touch ${HOME}/.gcloud-ansible-bash_history
  chmod 600 ${HOME}/.gcloud-ansible-bash_history
  docker run -it --rm \
    -v ${HOME}/.gcloud-ansible-bash_history:/root/.bash_history \
    -v ${SSH_AUTH_SOCK}:${SSH_AUTH_SOCK} \
    -e SSH_AUTH_SOCK="${SSH_AUTH_SOCK}" \
    -v $HOME/.config/gcloud:/home/root/.config/gcloud:ro \
    -v $HOME/.ssh:/home/root/.ssh \
    --name ansible \
    mccurdyc/ansible:latest "$@"
}
```

## TODOs

- [ ] pin all Ansible dependencies via pip and a virtualenv.
- [ ] use [wagoodman/dive](https://github.com/wagoodman/dive) to see how the Dockerfile layer caching could be improved.
