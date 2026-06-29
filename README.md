FROM ubuntu:22.04

# Hindari interaksi saat instalasi
ENV DEBIAN_FRONTEND=noninteractive

# Install XFCE, Wine, dan aplikasi pendukung
RUN apt-get update && apt-get install -y \
    xfce4 xfce4-goodies xrdp \
    wine64 winetricks xvfb \
    && apt-get clean

# Konfigurasi user
RUN useradd -m -s /bin/bash tuan && \
    echo "tuan:password123" | chpasswd && \
    adduser tuan sudo

# Konfigurasi XRDP
RUN echo xfce4-session > /home/tuan/.xsession
RUN echo "xfce4-session" > /etc/skel/.xsession

EXPOSE 3389

# Menjalankan XRDP di latar belakang
CMD ["/usr/sbin/xrdp", "-n"]

