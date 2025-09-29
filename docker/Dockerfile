# ARM64-friendly base for M2
FROM ubuntu:24.04

# Avoid interactive tzdata prompts
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    openssh-server sudo python3 python3-apt \
  && rm -rf /var/lib/apt/lists/*

# Create Ansible user with passwordless sudo
RUN useradd -m -s /bin/bash ansible \
  && echo "ansible ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/ansible \
  && chmod 0440 /etc/sudoers.d/ansible

# SSH setup
RUN mkdir -p /var/run/sshd /home/ansible/.ssh
# Inject pubkey at build time
ARG PUBKEY=""
RUN echo "${PUBKEY}" > /home/ansible/.ssh/authorized_keys \
  && chown -R ansible:ansible /home/ansible/.ssh \
  && chmod 700 /home/ansible/.ssh \
  && chmod 600 /home/ansible/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd","-D","-e"]