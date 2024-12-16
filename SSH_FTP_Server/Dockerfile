FROM ubuntu:latest

# Instalar paquetes necesarios para SSH y FTP
RUN apt-get update && apt-get install -y \
    openssh-server \
    vsftpd \
    && rm -rf /var/lib/apt/lists/*

# Configuración para SSH
RUN mkdir /var/run/sshd
RUN echo 'root:password123' | chpasswd
RUN sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Configuración para FTP
RUN sed -i 's/anonymous_enable=YES/anonymous_enable=NO/' /etc/vsftpd.conf
RUN echo "local_enable=YES" >> /etc/vsftpd.conf
RUN echo "write_enable=YES" >> /etc/vsftpd.conf
RUN echo "chroot_local_user=YES" >> /etc/vsftpd.conf
RUN echo "allow_writeable_chroot=YES" >> /etc/vsftpd.conf  # Permitir chroot con directorio raíz escribible
RUN echo "pasv_promiscuous=YES" >> /etc/vsftpd.conf
RUN echo "pasv_enable=YES" >> /etc/vsftpd.conf
RUN echo "pasv_min_port=10000" >> /etc/vsftpd.conf
RUN echo "pasv_max_port=10100" >> /etc/vsftpd.conf
RUN echo "pasv_address=127.0.0.1" >> /etc/vsftpd.conf  # Cambia esta dirección si accedes desde una red externa

# Crear usuario para FTP
RUN useradd -m -s /bin/bash ftpuser && echo "ftpuser:ftp123" | chpasswd

# Ajustar permisos del directorio del usuario FTP
RUN chmod a-w /home/ftpuser && mkdir /home/ftpuser/files && \
    chown ftpuser:ftpuser /home/ftpuser/files && chmod 755 /home/ftpuser/files

# Exponer los puertos SSH (22) y FTP (21)
EXPOSE 22 21

# Script para iniciar los servicios
CMD service ssh start && service vsftpd start && tail -f /dev/null