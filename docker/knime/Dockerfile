# This docker image is intented to fire up a fully functional 
# Environment for knime on linux, this is because if for example
# You are running on a very new linux distro, there are some well
# known issues with the GTK libraries that make knime run poorly

FROM ubuntu:14.04

MAINTAINER Luis Eduardo Ferro Diez <luisedof10@gmail.com>

# Install dependencies then create the knime user
RUN apt-get update -y &&  \
	apt-get install -y xterm firefox libgtk2.0-0 libswt-gtk-3-jni \
	libswt-gtk-3-java libswt-gnome-gtk-3-jni libwebkitgtk-1.0-0 libwebkitgtk-3.0-0 && \
	useradd -c 'Knime User' -m -d /home/knime -s /bin/bash knime

ENV TERM=xterm

# Setup gnome desktop environment to get all the libraries to make this look good
RUN apt-get install -y gnome-shell ubuntu-gnome-desktop

# Copy the knime installer downloaded separately
ADD assets /home/knime

# Working dir will be the knime user home
WORKDIR /home/knime

# From now on, we just need to work with knime user
USER knime

# Expand the knime workbench
RUN tar -xvzf $(ls)

# Bash as entrypoint to avoid messing around with different knime versions at startup
ENTRYPOINT ["bash"]

# docker image build -t <knime_image_tag> .
# docker container run -it --name knime -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v <some_folder>:/home/knime/workspace <knime_image_tag>
# $/home/knime<version>/knime