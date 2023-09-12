# Use an existing docker image for Ubuntu with a desktop environment and noVNC
FROM dorowu/ubuntu-desktop-lxde-vnc

# Install SSH server
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd

# Set root password for SSH
RUN echo "root:$SSH_PASSWORD" | chpasswd

# Enable SSH login for root
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# Expose SSH port and noVNC port
EXPOSE 22 80

# Start SSH server
CMD ["/usr/sbin/sshd", "-D"]