# Use the official Almalinux base image
FROM debian:latest

# Install OpenSSH server and any required dependencies
RUN apt update && apt upgrade -y && apt install -y openssh-server  iproute2 python3 && \
    mkdir /var/run/sshd

# Set the root password
RUN echo 'root:password' | chpasswd

# Set up SSH for key-based authentication
RUN mkdir -p /root/.ssh && \
    chmod 700 /root/.ssh

# Copy the SSH public key to the root user's authorized keys
COPY id_rsa.pub /root/.ssh/authorized_keys

# Set permissions for the authorized keys file
RUN chmod 600 /root/.ssh/authorized_keys

# Generate SSH host keys
RUN ssh-keygen -A

# Expose port 22 for SSH
EXPOSE 22

# Keep the container running by starting the SSH service
CMD ["/usr/sbin/sshd", "-D"]
