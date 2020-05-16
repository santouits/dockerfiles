FROM ubuntu
LABEL maintainer "github.com/santouits"


RUN apt update \
    && apt install \
        -y --no-install-recommends \
    	libgl1-mesa-dri \
    	libgl1-mesa-glx \
	libxi6 \
	libxinerama1 \
    	libxcursor1 \
    	libxrandr2 \
	libasound2 \
	libpulse0 \
	wget \
	procps \
	ca-certificates \
	unzip \
    && mkdir /spam && cd /spam \
    && wget https://downloads.tuxfamily.org/godotengine/3.2.1/Godot_v3.2.1-stable_x11.64.zip \
    && unzip Godot_v3.2.1-stable_x11.64.zip \
    && rm Godot_v3.2.1-stable_x11.64.zip \
    && mv God* /usr/bin/godot \
    && cd / \
    && rm -rf /spam \
    && apt remove -y unzip wget --autoremove \
    && rm -rf /var/lib/apt/lists/*

ENV USERNAME gamedev
ENV HOME /home/$USERNAME

RUN useradd --create-home --home-dir $HOME $USERNAME \
	&& chown -R $USERNAME:$USERNAME $HOME \
	&& usermod -a -G audio,video $USERNAME

ADD init $HOME

WORKDIR $HOME
USER $USERNAME

ENTRYPOINT [ "bash", "init" ]
