# Minimal "server" image used for all lab nodes.
# Deliberately close to a bare cloud image: just Python (Ansible's only hard
# requirement on a managed node) + sudo + basic networking tools.


FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3 \
    python3-apt \
    sudo \
    iproute2 \
    ; \
    ln -sf /usr/bin/python3 /usr/bin/python \
    ; \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# keep the container alive so ansible has something to execute into 
CMD [ "tail", "-f", "/dev/null" ]