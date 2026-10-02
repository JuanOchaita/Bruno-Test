# Jenkins LTS con bru (Bruno), uv con Python 3.12 y el CLI de docker.
# El CLI de docker habla con el motor del host por el socket montado en
# /var/run/docker.sock.
# Sin USER jenkins al final: corre como root para poder usar ese socket.
FROM docker.io/jenkins/jenkins:lts-jdk21

USER root
RUN apt-get update \
 && apt-get install -y --no-install-recommends nodejs npm \
 && rm -rf /var/lib/apt/lists/* \
 && npm install -g @usebruno/cli \
 && bru --version

COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /usr/local/bin/
COPY --from=docker.io/library/docker:cli /usr/local/bin/docker /usr/local/bin/
ENV UV_PYTHON_INSTALL_DIR=/opt/uv-python
RUN uv python install 3.12 && chmod -R a+rX /opt/uv-python
