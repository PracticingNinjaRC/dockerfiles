FROM ubuntu:16.04

LABEL "Maintainer"="Scott Hansen <firecat4153@gmail.com>"

ENV DEBIAN_FRONTEND noninteractive
ENV SABNZBD_USER sabnzbd
ENV UID 22000

COPY start.sh /start.sh
RUN gpg --keyserver keys.gnupg.net --recv-keys 4BB9F05F && \
    gpg --armor --export 4BB9F05F | apt-key add - && \
    echo "deb http://ppa.launchpad.net/jcfp/ppa/ubuntu xenial main" >> /etc/apt/sources.list && \
    echo "deb http://ppa.launchpad.net/jcfp/sab-addons/ubuntu xenial main" >> /etc/apt/sources.list && \
    apt-get -q update && \
    apt-get install -qy \
        sabnzbdplus \
        ca-certificates \
        locales \
        python-sabyenc \
        par2-tbb \
        unrar && \
    useradd --no-create-home -g users --uid $UID $SABNZBD_USER && \
    chmod +x /start.sh && \
    rm -rf /var/lib/apt/lists/* && \
    locale-gen en_US.UTF-8

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

USER $SABNZBD_USER

CMD ["/start.sh"]
