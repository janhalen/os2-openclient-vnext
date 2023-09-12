# Use an existing docker image for Ubuntu with a desktop environment and noVNC
FROM dorowu/ubuntu-desktop-lxde-vnc

# Add missing GPG key and install SSH server
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
    apt-get update && \
    apt-get install -y openssh-server

RUN mkdir /var/run/sshd

# Set root password for SSH
RUN echo 'root:ansiblesemaphore' | chpasswd

# Enable SSH login for root
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose SSH port and noVNC port
EXPOSE 22 80

# Create a new script that will start sshd and then run whatever command was passed to the container
RUN echo '#!/bin/bash\n\
service ssh start\n\
exec "$@"' > /entrypoint.sh && chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["/usr/sbin/sshd", "-D"]