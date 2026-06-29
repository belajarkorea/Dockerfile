# Dockerfile
FROM ubuntu:22.04

# Install XFCE4, XRDP, dan kebutuhan RDP lainnya
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y \
    xfce4 xfce4-goodies xrdp tightvncserver \
    && apt-get clean

# Konfigurasi user
RUN useradd -m -s /bin/bash ErickDrfile && \
    echo "TuanEri:TuanEri@2026!" | chpasswd && \
    adduser TuanEri sudo

# Konfigurasi XRDP
RUN echo xfce4-session > /etc/skel/.xsession
RUN echo "xfce4-session" > /home/TuanSebastian/.xsession

EXPOSE 3389

# Jalankan XRDP saat container mulai
CMD ["/usr/sbin/xrdp", "-n"]
