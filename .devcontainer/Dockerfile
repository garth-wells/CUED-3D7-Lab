FROM mcr.microsoft.com/devcontainers/miniconda:3

RUN export DEBIAN_FRONTEND=noninteractive && \
    sudo apt-get -qq update && \
    sudo  apt-get -yq --with-new-pkgs -o Dpkg::Options::="--force-confold" upgrade && \
    sudo  apt-get -y install xvfb && \
    sudo  apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Copy environment.yml (if found) to a temp location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && /opt/conda/bin/conda env create -f /tmp/conda-tmp/environment.yml; fi \
    && rm -rf /tmp/conda-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
