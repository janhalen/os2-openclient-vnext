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
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Create a supervisor conf for sshd
RUN echo '[program:sshd]\n\
command=/usr/sbin/sshd -D\n\
autostart=true\n\
autorestart=true\n\
redirect_stderr=true' > /etc/supervisor/conf.d/sshd.conf

# Expose SSH port
EXPOSE 22 80

# Run supervisor
CMD ["/usr/bin/supervisord"]