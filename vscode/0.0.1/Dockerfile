FROM debian:8

LABEL Maikon Canuto

ENV DEBIAN_FRONTEND noninteractive  

RUN apt-get update -y &&\
    apt-get install -y --force-yes \
    apt-transport-https \
    sudo \
    curl \ 
    libgtk2.0-0 \
    libgconf2-4 \
    libnss3 \
    libxtst6 \
    libcanberra-gtk-module \
    libgl1-mesa-glx \
    libxss1

RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg && \
    install -o root -g root -m 644 packages.microsoft.gpg /usr/share/keyrings/ && \
    sh -c 'echo "deb [arch=amd64 signed-by=/usr/share/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'

RUN apt-get update -y && \
    apt-get install -y --force-yes code && \
    apt-get autoremove -y && \
    apt-get autoclean -y

RUN cp /usr/lib/x86_64-linux-gnu/libxcb.so.1 /usr/share/code/ &&\
    cp /usr/lib/x86_64-linux-gnu/libxcb.so.1.1.0 /usr/share/code/ &&\
    sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/share/code/libxcb.so.1 &&\
    sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/share/code/libxcb.so.1.1.0

RUN mkdir /.vscode

ENTRYPOINT /usr/bin/code --user-data-dir=/.vscode --verbose 